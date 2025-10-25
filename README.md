# GoWest 2025

[GoWestConf.com](https://www.gowestconf.com/)

| time  | link                                                                                                                                                                      |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 10:15 | [Building Production Grade AI in Go: a Live Post-mortem](#building-production-grade-ai-in-go-a-live-post-mortem)                                                          |
| 11:00 | [Fundamentals of Memory Management in Go: Learning Through the History](#fundamentals-of-memory-management-in-go-learning-through-the-history)                            |
| 11:30 | [Spot the Nil Dereference: How to avoid a billion-dollar mistake](#spot-the-nil-dereference-how-to-avoid-a-billion-dollar-mistake)                                        |
| 14:00 | [Conduit: Real-Time Data Streams Made Simple (and Fast) with Go](#conduit-real-time-data-streams-made-simple-and-fast-with-go)                                            |
| 14:30 | [Go Channels Demystified](#go-channels-demystified)                                                                                                                       |
| 16:00 | [The basics of "go/ast" for people who can't even spell ast](#the-basics-of-goast-for-people-who-cant-even-spell-ast)                                                     |
| 16:30 | [You're already running my code in production: My journey to become a Go contributor](#youre-already-running-my-code-in-production-my-journey-to-become-a-go-contributor) |

## Building Production Grade AI in Go: a Live Post-mortem

Don't use Go for full AI model training and inference.
Use a language that is designed for it, like Python.

Go works great for concurrency AI request handling.
You can use Go to build a small API that can handle a lot of requests in parallel.

## Fundamentals of Memory Management in Go: Learning Through the History

Stack frame is a LIFO - First in, last out.
Google "ABI" to learn more about the Application Binary Interface.

Each scope creates it's own stack frame.

Heap is a memory area that can be accessed by different scopes.
The stack uses a pointer to the heap to access the data. `v := make([]int, 10)` creates a slice on the heap.

Go has a different garbage collector than other languages.
Most languages work where all non primitive values are on the heap.
Go uses Heap escape analysis to determine if a value is on the heap or the stack.

`go build -gcflags="-m -l" *.go` will show you the Heap escape analysis.

Talked about an article that cut memory by half & CPU usage by 99%.
When filtering a list, rather than creating a new list, she used the original list and assigned values to the existing list.

## Spot the Nil Dereference: How to avoid a billion-dollar mistake

You can use the same var name in different scopes.
It won't modify the outer scope.
So look out for creating a new variable with the same name when using `:=` in a scope.

**Converting a nil pointer to an interface results in a zero value, NOT nil.**

Don't use an Error interface in the return type.
You can still return a custom error interface but the function signature shouldn't use the Error interface.

Recommends book "100 Go Mistakes and How to Avoid Them"

## Conduit: Real-Time Data Streams Made Simple (and Fast) with Go

[Conduit](https://github.com/ConduitIO/conduit?tab=readme-ov-file#readme) is an open source Go-based streaming engine.
Simplify real-time data pipelines.
Uses Goroutines & Channels.
Contains a CLI for managing pipelines & streaming.

## Go Channels Demystified

Keep in mind that channels are just in-memory queues.

> Closing a channel just says "I'm done sending messages on this channel", you can still read from the closed channel.

If doing async read (with a buffered channel), you must start the read goroutine before sending messages to the channel.

Using channels _can_ help avoid locking and having to manage mutexes.

**TODO: I should implement this in the impact API ingestion**

## The basics of "go/ast" for people who can't even spell ast

## You're already running my code in production: My journey to become a Go contributor
