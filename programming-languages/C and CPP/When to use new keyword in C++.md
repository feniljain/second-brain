- If you use `new` keyword, it:
	- Allocates memory on heap
	- Programmer has to take care to `delete` it
	
- If you don't use new keyword
	- Memory is allocated on stack (tho too many objects on stack can cause stack overflow)
	- No need to call `delete`

- Let's say you want to return a pointer an object from a function, you should use `new`