- We want async for following reasons:
	- OS only does allocation in page sizes, i.e. one page, two page, etc. One can have a requirement of smaller stack with larger number of threads.
	- Second problem is setting relevant configs to achieve C10K on every machine, every time
	- Third problem is context switches between user and kernel space is expensive
	- Fourth problem is thread stack is static, we can't increase or decrease it.