# WASM Memory

- WASM uses a linear memory layout which is restricted to upper cap of 4 gigs
- They cannot control host's memory and are given a virtual space where this linear memory is alloacted
- This has major benefits like isolation (sandboxed envs for running each wasm module), runtime being able to keep memory usage in check.
- Tools like `wasm-bindgen` make a wrapper around js which let's both javascript and wasm use the same linear runtime.
- It is possible to interact with other wasm modules through import/export though capabilities are still limited.
- Interesting part is wasm can be written in many languages, how is it able to restrict its own memory model when each language has its own memory model? From what I understand is these need a layer and that's why we have language specific implementations for wasm. The article which I got this info from says this:

	"Simple. By understanding how allocations and deallocations are achieved when attempting to write/read from the host’s runtime and by taking into account and how to simplify the exchange across the varying complex data types."

  I do not completely understand what the person means here
- So there can be two ways in which memory is managed by the WASM:
	- manual
	- with the help of OS
	- WASM doesn't have an official garbage collector yet
- For the manual method it would convert into how we do things in C and C++
- For help of OS, what we do is we use the host's memory, but we copy it over every time to WASM's linear memory, this sounds inefficient.
- This gives me similar vibe to the bytecode VM we implemented for `lox` we implemented in `crafting interpreters` 

#wasm #memory-management