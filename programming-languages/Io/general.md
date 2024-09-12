- It's a prototype based GCed language
- Spelled always with a capital `I` followed by `o`
- all coding is done via slot-accesses i.e. message sends
- What is (a b c d) in Lisp is a(b, c, d) in Io.
- Io uses actors for concurrency. It also boasts on strong concurrency model.
- It evaluates function params lazily
- Everything is a message that returns another receiver
	- Each message takes optional
	- Each message returns an object
 - It also has good reflection support
 - It takes args first and then the method name to call then upon, for e.g. hello world printing looks like:
```
"hello world" print
```
- A better way to read it is: sending `print` message to string `"hello world"`
	- Receivers go on the left and messages go on the right
 - Objects have slots
	 - Think of slots as a hash
	 - Each slot is referred with the help of a key
  - You have an object ( let's say `A` ) and define a slot ( let's say `desc` ) on it
	  - Now next you clone the object ( let's say `B` )
		  - This does not clone slots to `B`
	  - When you send `desc` to `B` it actually queries `A` to determine value of `desc`
		  - This is true for as many levels as you want
	- _This is how Io’s object model works. Objects are just containers of slots. Get a slot by sending its name to an object. If the slot isn’t there, Io calls the parent._
   - Only objects with first character capital in name have `type` slot assigned to them
	   - Objects having `type` slot = `Types` in Io
- Methods in Io are also objects