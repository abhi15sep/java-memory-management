# java-memory-management

```bash
-Xmx  - Set maximum heap size.
-Xmx512m

-Xms  - Set the starting heap size
-Xms150m

-XX:MaxPermSize - Set the size of permgen (only till JAVA 7)
-XX:MaxPermSize=256M

-verbose:gc - print to the console when a garbage collection takes place.

-Xmn - Set the size of young generation. It is usually 1/3 of the heap size. Oracle suggests to keep it between 1/2 to 1/4 of heap size.
-Xmn256m

-XX: HeapDumpOnOutOfMemory - Creates a heap dump file.

Types of GC: While GC takes place application paused for a while. It doesn,t matter machine is single or multi-threaded.

1) Serial - uses single thread and suitable for small applications.
-XX:+UseSerialGC

2) Parallel - It performs GC on young generation called Minor GC. Multiple threads performs garbage collection. It is sometimes called throughput collector.
-XX:+UseParallelGC

3) Mostly Concurrent - It performs GC concurently. Stop the application during MARK phase and starts during SWEEP phase. "Stop the world" will not occur. Its of 2 types:
-XX:+UseConcMarkSweepGC
-XX:+UseG1GC 

To check your default garbage collector used in machine:
-XX:+PrintCommandLineFlags

To See runtime heap utilization use:
jvisualvm

Few Links listing all JVM flags.
https://www.oracle.com/technetwork/articles/java/g1gc-1984535.html
https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
https://medium.com/@krishankantsinghal/understanding-garbage-collection-using-visualvm-7e1520cb4ec0
https://medium.com/@hoan.nguyen.it/how-did-g1gc-tuning-flags-affect-our-back-end-web-app-c121d38dfe56
https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/index.html
```
## Should be tried in production
The above options have the following effect:
```bash
-Xms, -Xmx: Places boundaries on the heap size to increase the predictability of garbage collection. The heap size is limited in replica servers so that even Full GCs do not trigger SIP retransmissions. -Xms sets the starting size to prevent pauses caused by heap expansion.

-XX:+UseG1GC: Use the Garbage First (G1) Collector.

-XX:MaxGCPauseMillis: Sets a target for the maximum GC pause time. This is a soft goal, and the JVM will make its best effort to achieve it.

-XX:ParallelGCThreads: Sets the number of threads used during parallel phases of the garbage collectors. The default value varies with the platform on which the JVM is running.

-XX:ConcGCThreads: Number of threads concurrent garbage collectors will use. The default value varies with the platform on which the JVM is running.

-XX:InitiatingHeapOccupancyPercent: Percentage of the (entire) heap occupancy to start a concurrent GC cycle. GCs that trigger a concurrent GC cycle based on the occupancy of the entire heap and not just one of the generations, including G1, use this option. A value of 0 denotes 'do constant GC cycles'. The default value is 45.
```
