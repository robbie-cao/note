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

## Reference

- http://maxim.int.ru/bookshelf/PthreadsProgram/toc.html
