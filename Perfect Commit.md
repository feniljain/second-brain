#git

- Link: https://simonwillison.net/2022/Oct/29/the-perfect-commit/
- Perfect Commit is a single commit that contains all of the following:
	-   The **implementation**: a single, focused change
	-   **Tests** that demonstrate the implementation works
	-   Updated **documentation** reflecting the change
	-   A link to an **issue thread** providing further context
- Here `git blame` is the place from where you can get everything, git blame a line, get the commit, why that change was made, an issue linking to it which has documentation around all the decisions taken while making that change
- If your project defines APIs that are meant to be used outside of your project, they need to be documented. 
	- It is critical that this documentation **must live in the same repository as the code itself**.
- You want to document a lot of decisions you take while writing the code, link stackoverflow/forum questions to a specific part of code, use issues for that and link 