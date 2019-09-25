# Smart Pointer
  In computer science, a **smart pointer** is an abstract data type that simulate a pointer while
providing added features, such as *automatic memory management* or *bounds checking*.<br>
  Pointer misuse can be a major source of bugs. Smart pointer prevent most situations of memory
leaks by making the *memory deallocation* automatic.<br>

## C++ Smart Pointer
  In C++, **smart pointer** is implemented as a template class that mimics, by means of operator
overloading, the behaviors of a traditional *raw pointer*, (e.g. dereferencing, assignment) while
providing additional memory management features.<br>

## Motivation
  With raw pointer, the programmer need to explicitly delete memory, but it may not goes well.
<br>
```
MyObject* ptr = new MyObject();
ptr->DoSomething();
delete ptr;
// Wait, what if DoSomething() raise an exception ...?
```
  With **Smart Pointer**, we can avoid this.
```
{
  SmartPointer<MyObject> ptr(new MyObject());
  ptr->DoSomething();
} // out of scope, memory freed, even if exception is raised.
```

## Feature
  **Smart pointer** can facilitate *intentional programming* by expressing, in the type, how the
memory of the referent will be managed.<br>
<br>
  For example, if a C++ function returns a pointer, there is no way to know whether the caller
should *delete* the memory of the referent when the caller is finished with the information.<br>
    `SomeType* AmbiguousFunction()`
  Traditionally, *naming conventions* have been used to resolve the ambiguity, which is an 
error-prone, labor-intensive approach.<br>
<br>  
  C++ 11 introduced a way to ensure correct memory management in this case by declaring the
function to return a *unique_ptr*.<br>
    `std::unique_ptr<SomeType> ObviousFunction()` 
  The declaration of the function return type as *unique_ptr* makes explicit the fact that the
caller takes ownership of the result, and the C++ runtime ensures that the memory will be
reclaimed automatically.<br>

## unique_ptr
  C++ 11 introduces *std::unique_ptr* defined in the header <memory>.<br>
  A *unique_ptr* is a container for a raw pointer, which the *unique_ptr* is said to own. A
*unique_ptr* explicitly prevent copying of its contained pointer, but the std::move function can
be used to transfer ownership of the contained pointer to another *unique_ptr*.<br>
```
std::unique_ptr<int> p1(new int(5));
std::unique_ptr<int> p2 = p1; // Compile Error
std::unique_ptr<int> p3 = std::move(p1); // Transfer ownership. p3 owns the memory, p1 is nullptr.

p3.reset(); // Deletes the memory.
p1.reset(); // Does nothing.
```

### unique_ptr tips
  *std::unique_ptr* are useful when you want to tie the lifetime of an object to a particular block
or if you embedded it as member data inside another object, the lifetime of that other object.

## shared_ptr & weak_ptr
  C++ 11 introduces *std::shared_ptr* and *std::weak_ptr*, defined in the header <memory>.<br>
  A *shared_ptr* is a container for a raw pointer. It maintains **reference counting** ownership of
its contained pointer in cooperation with all copies of the *shared_ptr*. An object referenced
by the contained raw pointer will be destroyed when all copies have been destroyed.<br>
```
std::shared_ptr<int> p0(new int(5)); // valid, allocate 1 integer & init to 5
std::shared_ptr<int[]> p1(new int[5]); // valid, allocate 5 integers.
std::shared_ptr<int[]> p2 = p1; // Both now own the memory.

p1.reset(); // Memory still exist, due to p2.
p2.reset(); // Delete the memory, since no one owns it.
```
  A *weak_ptr* is a container for a raw pointer. It is created as a copy of a *shared_ptr*. The
existence or destruction of *weak_ptr* copies of a *shared_ptr* have no effect on the *shared_ptr*
or its other copies. After a *shared_ptr* have been destroyed, all *weak_ptr* copies becomes 
**empty**.<br>
```
std::shared_ptr<int> p1 = std::make_shared<int>(5);
std::weak_ptr<int> wp1 {p1}; // p1 owns the memory.

{
  std::shared_ptr<int> p2 = wp1.lock(); // Now p1 and p2 own the memory.
  if (p2) { // p2 is init from a weak pointer, so you have to check if it exist
    DoSomethingWith(p2);
  }
} // p2 is destroyed, Memory is owned by p1.

p1.reset(); // Delete the memory.

std::shared_ptr<int> p3 = wp1.lock(); // Memory is gone, so we get an empty shared_ptr
if (p3) { // code will not execute
  ActionThatNeedALivePointer(p3);
}
```

## shared_ptr & cicular reference
  There is one drawback to **reference counting pointers** -- the possibility of creating **circular
reference**.<br>
```
struct Owner {
  std::shared_ptr<Owner> other;
};

std::shared_ptr<Owner> p1 (new Owner());
std::shared_ptr<Owner> p2 (new Owner());
p1->other = p2; // p1 reference p2
p2->other = p1; // p2 reference p1
// Oops, the reference count of p1 and p2 never goes to 0!
```
  To work around this problem, *weak_ptr*(uncounted reference) can be used.
