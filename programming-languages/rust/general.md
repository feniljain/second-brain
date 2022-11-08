- Rust async is based on readiness (try X, if not ready tell me when it's ready to retry) which lends itself to epoll/kqueue, not completion (start X, return result immediately or tell me when X is completed) which is what io_uring and IOCP do.

	These completion based APIs are extremely awkward to do/expose safely in Rust which is why tokio by default doesn't use them. You end up having to either copy buffers around or pass owned, heap allocated buffers to them for IO since the APIs require stable address for the buffers in the face of arbitrary Future cancellation. [ Source: https://www.reddit.com/r/rust/comments/xcaoyl/what_is_the_point_of_using_async/ ]
	
- In terms of async #rustlang, a projection method is one which can be implemented to access fields of a pinned struct