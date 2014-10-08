---
layout: post
title: Concurrent Testing in Grails with GPars and Spock
categories:
- Articles
tags:
- Unit Testing, Integration Testing, Concurrency, Spock, Grails, GPars
status: publish
type: post
published: true 
meta:
  _publicize_pending: '1'
author: Sathish Hariharan
---

Last month I did a major backend refactoring of on of our applications and was feeling happy about how
 much the code has been simplified and easier to understand. All was well until suddenly, we started getting strange
errors in production. Our set of unit and integration tests had passed and I was quite confident that nothing
had broken.

With a few hours of debugging and head scratching, I nailed the problem down to some mutable variables that
were being shared across multiple threads and sessions. In order to avoid initiating and creating multiple
objects of a particular service, we had converted it to a Singleton, and the resulting change caused some
variables ending up shared between multiple threads and break down the complete application. We did not have
any unit or integration tests developed to test for concurrency and hence could not catch the issues earlier

This experience led me to write test cases for concurrency and subsequent evaluation of technologies appropriate
for developing concurrent applications. A few hours of reading opened my eyes to how much the world of
 concurrent programming for the JVM had changed in the last few years. My experience is core java were from
Java 2.0 years and with constructs like Thread, Runnable and Synchronized methods.

Java 5.0 has apparently changed the space completely with introduction of the new util.concurrent package. Here
are some of the things are now possible now when using the modern JDK

    * Manage your own thread pool using Executor Services
    * Use the concept of callable to asynchronously call and receive responses from thread
    * Coordinate threads using Countdown latches (similar to Semaphores in C++)
    * Better data structures for data exchange between threads - BlockingQueue
    * Collection data structures - ConcurrentQueue, ConcurrentHashmap for better performance
    * Better granularity in synchronizing blocks of code (rather than using object level 'synchronized' methods) using Locks

Further exploring the topic I came across new libraries that were available to implement concurrency using
implementation patterns like Memory Transactions and Actors. The prominent ones for the JVM were Akka and GPars.

Akka is implemented in Scala and supports both of the patterns mentioned - it supports software transactional
memory (STM) by using specialized transactional primitives that can be modified only within defined transactions.
It also supports the concept of defining Actors - Objects that extended an Actor Object would always have their
methods executed in separate threads. The Actor pattern of concurrency is also supported by the Groovy GPars
library.

Since Grails obviously played best with Groovy, and also since the implementation of concurrent did not involve
 complex synchronizations, I chose to implement concurrent Spock tests using GPars. The combination of Spock's
 highly expressive specification language and the clean design of GPars makes writing tests quite enjoyable.

For example Spock allows Data Driven testing and allows you to wite tests like

    class MathSpec extends Specification {
        def "maximum of two numbers"() {
            expect:
            // exercise math method for a few different inputs
            Math.max(1, 3) == 3
            Math.max(7, 4) == 7
            Math.max(0, 0) == 0
        }
    }

GPars allows you to implement concurrent execution with a pool of threads and groovy collections like so:

    withPool {
        def selfPortraits = images
            .findAllParallel{it.contains me}
            .collectParallel {it.resize()}
    }

Combining these two results is extremely intuitive parallel test cases. I have included one of our example test
cases below:

    package com.squareprism.xyz

    import grails.test.mixin.TestMixin
    import grails.test.mixin.support.GrailsUnitTestMixin
    import spock.lang.Specification
    import static groovyx.gpars.GParsPool.*

    /**
     * See the API for {@link grails.test.mixin.support.GrailsUnitTestMixin} for usage instructions
     */
    @TestMixin(GrailsUnitTestMixin)
    class ParallelXYZGeneratorSpec extends Specification {

        // data array for test data
        def dataArray = [
                [11.26, 75.78, 25, 11, 1973, 4, 55],
                [11.26, 75.78, 25, 11, 1973, 4, 55],
                [11.26, 75.78, 25, 11, 1973, 4, 55],
                [11.26, 75.78, 25, 11, 1973, 4, 55],
                [11.26, 75.78, 25, 11, 1973, 4, 55],
                [11.26, 75.78, 25, 11, 1973, 4, 55],
                [11.26, 75.78, 25, 11, 1973, 4, 55],
                [11.26, 75.78, 25, 11, 1973, 4, 55]
        ]
        def results // collect results here

        def setup() {
        }

        def cleanup() {
        }

        void "test Parallel XYZ Generation"() {
            given:
            withPool(8) { // use 8 parallel threads
                results = dataArray.collectParallel{
                    return XYZGenerator.calculate(it[0], it[1], it[2], it[3], it[4], it[5], it[6])
                }
            }


            expect:
                results.size() == 8

        }
    }


