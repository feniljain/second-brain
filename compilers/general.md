[]()- A stack spill is passing parameters on the stack instead of in registers. It's unavoidable when the number of parameters exceeds the number of registers available for passing parameters (the parameters spill over onto the stack) or if the parameters don't fit into the registers.
	- Maybe this is why it's advised to not have parameters greater than 5 or 6? Coz then it becomes a performance hit, you need to check registers and stack both.
- Tail Calls ( for good explanation: https://blog.reverberate.org/2021/04/21/musttail-efficient-interpreters.html )
	- Calling another function at the end of a function
	- uses `jmp` assembly code instead of `call` ( call requires maintaining a lot of overhead stuff )
	- Tries to avoid stack spill by keeping all the parameters in register itself
	- So when you make call to another function, we don't need to replace registers with new values, as they already contain the values needed, this makes calling another functions extremely fast
	- And also takes stack memory usage from O(n) to O(1), and this is implemented in most functional languages, this is how they promote calling functions a lot.