# Garbage Collector
- Garbage collectors were first implement in Lisp, which was actually the second high-level language ever implemented(first being fotran)

- First ever GC implemented was a mark and sweep GC
	- As names suggest it contains two phases: Marking the objects and then sweeping off(reclaiming) their allocated memory,
	
- We first transverse each and every object present and mark them

- At the end all those nodes which are unmarked are recycled

- It becomes sometimes a bit complicated with pointers because the can in turn point to an object.

- What we do in such cases is a tricolor abstraction(this model also helps in incremental GCs)
	- Three colors being white, gray and black
	- White denotes node hasn't been visited
	- Gray denotes, node has been visited but not all it's references are resolved yet(for eg. a struct containing a pointer to a heap allocated object which in turn may contain other heap allocated structures). These objects are added to a new list called worklist (The set of objects we know about but we haven't processed yet).

	So if the object dereferenced contains another object that will be added to worklist too(maybe later too).

	- Black denotes all its children(including nested references) and this node itself are marked.
	
- Tracing GC does this job of marking objects which are behind references.

- GCs have two metrics to measure their performance: throughput and latency.
	- Throughput is the ability to not damage the time spent executing user code, so that more and more work can be done and hence more throughput.
	- Latency is the amount of time spent in **a** GC cycle.
	- Ideally we would like to maximize throughput and minimize latency.

#gc