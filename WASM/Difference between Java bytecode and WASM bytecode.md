# Java VS WASM Bytecode
- Java bytecode uses symbols for referencing identifiers, but WASM bytecode VM uses  indexes(much like crafting interpreter's `lox` VM).
- Java bytecode relies on automatic garbage collection, no such thing exists in WASM. ( a proposal does exist )
- Java bytecode is type-safe, in WASM it is direct cast as it can contain any type.
- Java bytecode does not access memory directly, WASM always access memory directly (linear memory allocated to it in a VM).
- Java bytecode has support for shared memory computing, while WASM only supports sequential access yet.

#bytecode #wasm #java