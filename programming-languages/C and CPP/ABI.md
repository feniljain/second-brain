# ABI
- C ABI is composed of two things, how compiler lays out:
	- the position, order, and layout of members in a struct
	- the argument types and return type of a function
- Okay, so in C we can break ABI just by having the wrong types on a function and not matching it up with a declaration. The linker genuinely doesn’t care about types or any of that nonsense. If the symbol `do_stuff` exists, it will bind to the symbol `do_stuff`.