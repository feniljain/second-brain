# eBPF
## General
- llvm `MCJIT` converts llvm IR to BPF bytecode

## Commands
- eBPF Commands can be divided into three categories:
	- Commands for working with BPF programs
	- Commands for working with BPF maps
	- And commands for working with both (collectively known as **objects**)

- BPF_CALL is used to call internal kernel helper functions (cannot call module helper functions)
- BPF_PROG_LOAD to load the programs

## Maps
- eBPF uses maps as a data structure to communicate between different BPF programs/kernel/user-space.
- It is manipulated using bpf() system call
- Has methods like bpf_lookup_elem() and map_update_elem() to play around with them.
- Each map has 4 defining values:
	- A type
	- Maximum number of elements
	- `value` size in bytes
	- `key` size in bytes