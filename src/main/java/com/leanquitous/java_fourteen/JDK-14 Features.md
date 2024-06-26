### Source 


#### Features
* 305:	Pattern Matching for instanceof (Preview)
* 343:	Packaging Tool (Incubator)
* 345:	NUMA-Aware Memory Allocation for G1
* 349:	JFR Event Streaming
* 352:	Non-Volatile Mapped Byte Buffers
* 358:	Helpful NullPointerExceptions
* 359:	Records (Preview)
* 361:	Switch Expressions (Standard) - Demo already done during JDK 12 included everything in demo.
* 362:	Deprecate the Solaris and SPARC Ports
* 363:	Remove the Concurrent Mark Sweep (CMS) Garbage Collector
* 364:	ZGC on macOS
* 365:	ZGC on Windows
* 366:	Deprecate the ParallelScavenge + SerialOld GC Combination
* 367:	Remove the Pack200 Tools and API
* 368:	Text Blocks (Second Preview)
* 370:	Foreign-Memory Access API (Incubator)

### Pattern Matching for instanceof (Preview)
Practical example done.

### Packaging Tool (Incubator)
Create a tool for packaging self-contained Java applications.

### NUMA-Aware Memory Allocation for G1
NUMA - Non uniform memory access

Improve G1 performance on large machines by implementing NUMA aware memory allocation.
Modern multi-socket machines increasingly have non-uniform memory access (NUMA), that is,
memory is not equidistant from every socket or core. Memory accesses between sockets have 
different performance characteristics, with access to more-distant sockets typically having more latency.

The parallel collector, enabled by by -XX:+UseParallelGC, has been NUMA-aware for many years. 
This has helped to improve the performance of configurations that run a single JVM across multiple 
sockets. Other HotSpot collectors have not had the benefit of this feature, which means they have 
not been able to take advantage of such vertical multi-socket NUMA scaling. Large enterprise 
applications in particular tend run with large heap configurations on multiple sockets, yet they 
want the manageability advantage of running within a single JVM. Users who use the G1 collector 
are increasingly running up against this scaling bottleneck.

### JFR Event Streaming
Expose JDK Flight Recorder data for continuous monitoring.

The HotSpot VM emits more than 500 data points using JFR, most of them not available through 
other means besides parsing log files. To consume the data today, a user must start a recording, 
stop it, dump the contents to disk and then parse the recording file. This works well for 
application profiling, where typically at least a minute of data is being recorded at a time, 
but not for monitoring purposes.

### Non-Volatile Mapped Byte Buffers
Add new JDK-specific file mapping modes so that the FileChannel API can be used to create 
MappedByteBuffer instances that refer to non-volatile memory.

### Helpful NullPointerExceptions
Improve the usability of NullPointerExceptions generated by the JVM by describing 
precisely which variable was null.

JVM now pinpoints to which method call/variable was null in the message during an NPE occurance.

### Records (Preview)
Records are compact syntax for declaring a classes which are transparent holders of shallowly 
immutable data. Records are a new kind of type declaration in the Java language.

The motivation to introduce this new type is to counter the argument of having to create a 
class kind of structure just to have the data carrier capabilities. 

A record has a name and a state description. The state description declares the components of the record. Optionally, a record has a body. For example:

        record Point(int x, int y) { }

Because records make the semantic claim of being simple, transparent holders for their data, a record acquires many standard members automatically:

* A private final field for each component of the state description;
* A public read accessor method for each component of the state description, with the same name and type as the component;
* A public constructor, whose signature is the same as the state description, which initializes each field from the corresponding argument;
* Implementations of equals and hashCode that say two records are equal if they are of the same type and contain the same state; and
* An implementation of toString that includes the string representation of all the record components, with their names.

### Deprecate the Solaris and SPARC Ports
Deprecate the Solaris/SPARC, Solaris/x64, and Linux/SPARC ports, with the intent to remove them in a future release.

### Remove the Concurrent Mark Sweep (CMS) Garbage Collector
Removing the CMS GC, we now have new G1 as the default one along with Shanendoah and ZGC alternatives for GC.

### ZGC on macOS
ZGC support for macOS.

### ZGC for windows (experimental)
ZGC support for windows.

### Deprecate the ParallelScavenge + SerialOld GC Combination
Deprecate the combination of the Parallel Scavenge and Serial Old garbage collection algorithms.
There is one combination of GC algorithms that we believe is very little used but requires a significant 
amount of maintenance effort

### Remove the Pack200 Tools and API
Pack200 is a compression scheme for JAR files. Remove the pack200 and unpack200 tools, and the 
Pack200 API in the java.util.jar package. These tools and API were deprecated for removal in Java SE 11

Pack200 was used to compress increasing java archives size so that the people can download 
easily and can adapt Java easily. But now time has changed we have significantly fast download speed 
and hence this is no longer a problem that we face. 

Pack200 is complex and file format is tightly coupled with class file and jar file format. Also pack200 
was used for client application (applet) to compress which is deprecated and no longer required.

### Text Blocks (Second Preview) (Demo already exists in JDK - 13)

### Foreign-Memory Access API (Incubator)
Introduce an API to allow Java programs to safely and efficiently access foreign memory outside of the 
Java heap. 

Many existing Java libraries and programs access foreign memory, for example Ignite, mapDB, memcached, 
and Netty's ByteBuf API. By doing so they can

* Avoid the cost and unpredictability associated with garbage collection (especially when maintaining 
large caches)
* Share memory across multiple processes, and
* Serialize and deserialize memory content by mapping files into memory (via, e.g., mmap).

Yet, the Java API does not provide a satisfactory solution for accessing foreign memory.

Java 1.4, allows the creation of direct byte buffers, which are allocated off-heap, and 
allows users to manipulate off-heap memory directly from Java. Direct buffers are, 
however, limited. For instance, it is not possible to create a buffer that is larger 
than two gigabytes.

