- Article: https://www.thecodedmessage.com/posts/raii/
	- RAII is a terrible name, better is OBRM = Ownership-Based Resource Management
	- What we want to prevent when compared to C:
		- Memory Leaks
		- Memory Corruption
		- Dangling Pointers/References
	- C++'s RAII only solved problem of leaks, but it did not address memory corruption or keeping allocations long enough
		- The system of move was introduced in C++ 11
	- Rust's RAII uses moves, borrows ( along with borrow checker ), and places where both fail we have reference counted structures
		- And for usecases none of them satisfy, `unsafe` ftw :)
	- Rust's RAII is a area between manual  memory management and GCed languages
	- Rust's move mechanisms as good as they are, can prove problematic in certain applications. As kernel devs don't want their memory moving automatically. Rust's solution for this was to introduce pinning which prevents a memory from moving.  This is useful in async and for kernel devs too. ( Tho kernel devs have some reservations with pinning too, more in this [tweet](https://twitter.com/fenil_jain_/status/1589134037188481024)  )
	- Memory leaks while using reference counted structures is something which is currently not preventable in any ways. So even Rust suffers from that.