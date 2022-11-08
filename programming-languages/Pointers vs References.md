# Pointer vs References
- Pointers have their own memory space and identity, they are separate variables, we can apply sizeof() on a pointer variable, but references are, simply put, an alias for a variable, just another name. So when we apply sizeof() on a reference, it gives information about the data it is references to (and hence any changes made to references are reflected in original variable).
- As pointer are another variables, they can be modified to point to another variable at any point, but references once initialised cannot be made to reference another variable.
- References also cannot be late initialized.
- A pointer can be bound to nullptr, but this is not allowed for reference (there are ways to do this, but it results in UB).
- Pointers can be dereferenced by using `*` and if fields of a struct need to be accessed we use `->` but with reference we can access the underlying variable directly (i.e. in case of field access of a struct, we use `.` as we do normally).
- One thing which is advantageous in references is that const references can be bound to temporaries, pointers cannot do this **directly**. This is one of the reasons `const &` is more convenient to use in argument lists.
- Pointers can be used as array variables too, we can just simple `++` and we have next element with us.
- References cannot be put in an array, while pointers can.

#basic-cs #pointers #references