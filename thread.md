# Threaded Programming

## Threaded Program Models

- The boss/worker model
- The peer model
- The pipeline model

> http://maxim.int.ru/bookshelf/PthreadsProgram/htm/r_19.html

## Boss/Worker Model

![](http://maxim.int.ru/bookshelf/PthreadsProgram/img/02FIG01_0.gif)

```c
main() /* The boss */
{
	forever {
		get a request
		switch request
		case X : pthread_create( ... taskX)
		case Y : pthread_create( ... taskY)
		.
		.
		.
	}
}

taskX() /* Workers processing requests of type X */
{
	perform the task, synchronize as needed if accessing shared resources
	done
}

taskY() /* Workers processing requests of type Y */
{
	perform the task, synchronize as needed if accessing shared resources
	done
}
```

## Peer Model

![](http://maxim.int.ru/bookshelf/PthreadsProgram/img/02FIG02_0.gif)

```c
main()
{
   	pthread_create( ... thread1 ... task1 )
   	pthread_create( ... thread2 ... task2 )
   	.
   	.
   	.
   	signal all workers to start
   	wait for all workers to finish
   	do any clean up
}
task1()
{
   	wait for start
   	perform task, synchronize as needed if accessing shared resources
   	done
}
task2()
{
	wait for start
   	perform task, synchronize as needed if accessing shared resources
   	done
}
```

## Pipeline Model

![](http://maxim.int.ru/bookshelf/PthreadsProgram/img/02FIG03_0.gif)

```c
main()
{
	pthread_create( ... stage1 )
	pthread_create( ... stage2 )
	.
	.
	.
	wait for all pipeline threads to finish
	do any clean up
}
stage1()
{
	forever {
    	get next input for the program
        do stage 1 processing of the input
        pass result to next thread in pipeline
    }
}
stage2()
{
	forever {
        get input from previous thread in pipeline
        do stage 2 processing of the input
        pass result to next thread in pipeline
    }
}
stageN()
{
	forever {
    	get input from previous thread in pipeline
        do stage N processing to the input
        pass result to program output
    }
}
```

## Buffering Data Between Threads

The boss/worker, peer, and pipeline are models for complete multithreaded programs. Within any of these models threads transfer data to each other using buffers. In the boss/worker model, the boss must transfer requests to the workers. In the pipeline model, each thread must pass input to the thread that performs the next stage of processing. Even in the peer model, peers may often exchange data.

A thread assumes either of two roles as it exchanges data in a buffer with another thread. The thread that passes the data to another is known as the producer; the one that receives that data is known as the consumer.

![](http://maxim.int.ru/bookshelf/PthreadsProgram/img/02FIG04_0.gif)

The ideal producer/consumer relationship requires:

- A buffer

  The buffer can be any data structure accessible to both the producer and the consumer. This is a simple matter for a multithreaded program, for a such a shared buffer need only be in the process's global data region. The buffer can be just big enough to hold one data item or it can be larger, depending upon the application.

- A lock

  Because the buffer is shared, the producer and consumer must synchronize their access to it. With Pthreads, you would use a mutex variable as alock.

- A suspend/resume mechanism

  The consumer may suspend itself when the buffer contains no data for it to consume. If so, the producer must be able to resume it when it places a new item in the buffer. With Pthreads, you would arrange this mechanism using a condition variable.

- State information

  Some flag or variable should indicate how much data is in the buffer.

```c
producer()
{
    .
    .
    .
    lock shared buffer
    place results in buffer
    unlock buffer
    wake up any consumer threads
    .
    .
    .
}
consumer()
{
    .
    .
    .
    lock shared buffer
    while state is not full {
        release lock and sleep
        awake and reacquire lock
    }
    remove contents
    unlock buffer
    .
    .
    .
}
```

Double buffering:

![](http://maxim.int.ru/bookshelf/PthreadsProgram/img/02FIG05_0.gif)

## Reference

- http://maxim.int.ru/bookshelf/PthreadsProgram/toc.html
