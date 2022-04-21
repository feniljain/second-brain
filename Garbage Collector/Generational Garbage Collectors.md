# Generational Garbage Collectors
### Motivation
- GCs spend a lot of time marking the objects, this is one of the slowest steps in a GC cycle. This is specially true for live objects, revisiting them is more waste of time, it just reduces throughput.

- What if there was a way we could tell which objects will longer than others and then not run mark phase for them as often?

### Solution
- GC researchers conducted a study on how long objects live in general, and noticed that if an object has lived long-enough, there's a higher chance for it to stick along for a longer time. In simpler terms, longer the object lives, higher is the chance it will be around for a good amount of time. Consequently we can reduce the time spent in marking it everytime (or run mark for it much less frequently).

- Now time to implement this is in GCs for real. The implementation is very simple, each object starts out in a special hotspot heap (name _nursery_). GC runs in this heap at a much higher frequency. Now let's say an object survives first mark phase, than it has increased its generation, it gets _tenured_. 

- After certain generations (usually one), it is shifted to another heap where long lived objects reside, this is  a place where GC runs comparatively less frequently. This saves a huge amount of time for GC runs and hence increasing their efficiency by magnitudes in right environments.

- Nurseries are also usually managed using a copying collector which is faster at allocating and freeing objects than a mark-sweep collector.