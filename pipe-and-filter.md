# Pipe and Filter

## Pipe and filter

A very simple, yet powerful architecture, that is also very robust. It consists of any number of components (filters) that transform or filter data, before passing it on via connectors (pipes) to other components. The filters are all working at the same time. The architecture is often used as a simple sequence, but it may also be used for very complex structures.

![](http://www.dossier-andreas.net/software_architecture/pipe_and_filter_2.jpg)

The **filter** transforms or filters the data it receives via the pipes with which it is connected. A filter can have any number of input pipes and any number of output pipes.

The **pipe** is the connector that passes data from one filter to the next. It is a directional stream of data, that is usually implemented by a data buffer to store all data, until the next filter has time to process it.

The **pump** or producer is the data source. It can be a static text file, or a keyboard input device, continously creating new data.

The **sink** or consumer is the data target. It can be a another file, a database, or a computer screen.

![](http://www.rantdriven.com/image.axd?picture=pipe-and-filters-concept.png)

## Sequence diagram

![](http://image.slidesharecdn.com/3-110513092437-phpapp01/95/3-architetture-software-architectural-styles-30-728.jpg?cb=1305278909)

> http://www.dossier-andreas.net/software_architecture/pipe_and_filter.html

## Pipes and filters pattern

![](https://i-msdn.sec.s-msft.com/dynimg/IC707853.png)

> https://msdn.microsoft.com/en-us/library/dn568100.aspx

## Reference

- http://www.eli.sdsu.edu/courses/spring04/cs635/notes/pipes/pipes.html
- http://www.dossier-andreas.net/software_architecture/pipe_and_filter.html
- http://www.slideshare.net/kronat/3-architetture-software-architectural-styles
- http://www.cs.sjsu.edu/~pearce/modules/patterns/distArch/pipeline.htm
