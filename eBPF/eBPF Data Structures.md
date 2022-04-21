# eBPF Data Structures
##  General
- 512 Byte Stack

##  Registers
- [[eBPF]] uses _eleven_ 64 bit with 32 bit subregisters.
- Registers range from `r0` - `r10`.
- `r10` is a read-only register containing frame pointer address (required for accessing the BPF stack space).
- A BPF program can call core kernel helper functions (not module ones), this is how registers are used here:
	- `r0` contains return value of the helper function call.
	- `r1`-`r5` contains arguments which will be passed on to the kernel helper function when call to them is made.
	- `r6`-`r9` are callee saved registers that will be kept throughout and after kernel helper function execution.
