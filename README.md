# CI311
Notes for CI311 exam.

## The Object Constraint Language

### Primitive Types

| Types   | Values            | Operators and Operations                                     |
| ------- | ----------------- | ------------------------------------------------------------ |
| Boolean | true, false       | =, <>, and, or, xor, not, implies, if-then-else-endif        |
| Integer | -3,0,6, ...       | =, <>, >, <, >=, <=, \*, +, - (unary), - (binary), / (real), abs( ), max(b), min(b), mod(b), div(b) |
| Real    | -1.2,0.1,1.3, ... | =, <>, >, <, >=, <=, \*, +, - (unary), - (binary), /, abs( ), max(b), min(b), round( ), floor() |
| String  | 'hello world'     | =, <>, size( ), concat(s2), substring(lower, upper), (1<=lower<=upper<=size), toReal( ), toInteger( ) |

### Collection and Tuple Types

| Description                               | Syntax                              | Examples                                                     |
| ----------------------------------------- | ----------------------------------- | ------------------------------------------------------------ |
| Abstract collection of elements of type T | Collection(T)                       |                                                              |
| Unordered collection, no duplicates       | Set(T)                              | Set{1,2}                                                     |
| Ordered collection, duplicates allowed    | Sequence(T)                         | Sequence{1, 2, 1}<br />Sequence{1..4} (same as Sequence{1, 2, 3, 4}) |
| Ordered collection, no duplicates         | OrderedSet(T)                       | OrderedSet{2, 1}                                             |
| Unordered collection, duplicates allowed  | Bag(T)                              | Bag{1, 1, 2}                                                 |
| Tuple (with named parts)                  | Tuple(field1 : T1, ...,fieldn : Tn) | Tuple{age : Integer = 5,<br />name : String = 'Joe'}<br />Tuple{name='Joe',age=5} |

**Note:** Tuple components can be accessed with "." e.g. 't1.name'

### Operations on Collection(T)

| Operation                                | Description                                                  |
| ---------------------------------------- | ------------------------------------------------------------ |
| size() : Integer                         | the number of elements in the collection.                    |
| count(o : T) : Integer                   | the number of occurrences of object *o* in the collection.   |
| includes(o : T) : Boolean                | true if object *o* is an element of the collection.          |
| includesAll(c : Collection(T)) : Boolean | true if all elements in the collection *c* are present in the current collection. |
| excludes(o : T) : Boolean                | true if object *o* is not an element of the collection.      |
| excludesAll(c : Collection(T)) : Boolean | true if all the elements in collection *c* are not present in the current collection. |
| isEmpty( ) : Boolean                     | true if the collection contains no elements.                 |
| notEmpty( ) : Boolean                    | true if the collection contains one or more elements.        |
| sum( ) : T                               | the addition of all the elements in the collection.          |

**Note:** Operations on collections are applied with "->" and not "."

### Operations on Set(T)

| Operation                                | Description                                                  |
| ---------------------------------------- | ------------------------------------------------------------ |
| =(s : Set(T)) : Boolean                  | true if *self* and *s* contain the same elements?            |
| union(s : Set(T)) : Set(T)               | The union of *self* and *s*. (Both sets combined together)   |
| union(b : Bag(T)) : Bag(T)               | The union of *self* and *s*.                                 |
| intersection(s : Set(T)) : Set(T)        | The intersection of *self* and *s*. (A set of elements which only appear in both sets) |
| intersection(b : Bag(T)) : Set(T)        | The intersection of *self* and *b*.                          |
| - (s : Set(T)) : Set(T)                  | The elements of *self*, which are not in *s*.                |
| including(object : T) : Set(T)           | The set containing all elements of *self* plus *object*.     |
| excluding(object : T) : Set(T)           | The set containing all elements of *self* minus *object*.    |
| symmetricDifference(s : Set(T)) : Set(T) | The set containing all the elements that are in *self* or *s*, but not in both. |
| flatten() : Set(T2)                      | If T is a collection type, the result is the set with all the elements of *self*; otherwise, the result is *self*. |
| asOrderedSet( ) : OrderedSet(T)          | OrderedSet with elements from *self* in undefined order.     |
| asSequence( ) : Sequence(T)              | Sequence with elements from *self* in undefined order.       |
| asBag( ) : Bag(T)                        | Bag with all elements from *self*.                           |

### Operations on Bag(T)

| Operation                         | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| = (b : Bag(T)) : Boolean          | True if *self* and *b* contain the same elements, the same number of times. |
| union(b : Bag(T)) : Bag(T)        | The union of *self* and *b*.                                 |
| union(s : Set(T)) : Bag(T)        | The union of *self* and set *s*.                             |
| intersection(b : Bag(T)) : Bag(T) | The intersection of *self* and *b*.                          |
| intersection(s : Set(T)) : Set(T) | The intersection of *self* and *b*.                          |
| including(object : T) : Bag(T)    | The bag with all elements of *self* plus *object*.           |
| excluding(object : T) : Bag(T)    | The bag with all elements of *self* minus *object*.          |
| flatten() : Bag(T2)               | If *T* is a collection type: bag with all the elements of all the elements of *self*; otherwise: *self*. |
| asOrderedSet( ) : OrderedSet(T)   | OrderedSet with elements from *self* in undefined order, without duplicates. |
| asSequence( ) : Sequence(T)       | Seq. with elements from *self* in undefined order.           |
| asSet( ) : Set(T)                 | Set with elements from *self*, without duplicates.           |

### Operations on Sequence(T)

| Operation                                                   | Description                                                  |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| = (s : Sequence(T)) : Boolean                               | True if *self* contains the same elements as *s*, in the same order. |
| union(s : Sequence(T)) : Sequence(T)                        | The sequence consisting of all elements in *self* followed by all elements in *s*. |
| flatten( ) : Sequence(T2)                                   | If *T* is a collection type, the result is the set with all the elements of all the elements of *self*; otherwise it's *self*. |
| append(object : T) : Sequence(T)                            | The sequence with all elements of *self*, followed by *object*. |
| prepend(object : T) : Sequence(T)                           | The sequence with *object*, followed by all elements in *self*. |
| insertAt(index : Integer, object : T) : Sequence(T)         | The sequence with *object*, followed by all elements in *self*. |
| subSequence(lower : Integer, upper : Integer) : Sequence(T) | The sequence consisting of *self* starting at index *lower*, up to and including index *upper*; (1 <= *lower* <= *upper* <= size). |
| at(i : Integer) : T                                         | The *i*-th element of *self*; (1 <= *i* <= size).            |
| indexOf(object : T) : Integer                               | The index of object in *self*.                               |
| first( ) : T                                                | The first element in *self*                                  |
| last( ) : T                                                 | The last element in *self*                                   |
| including(object : T) : Sequence(T)                         | The sequence containing all elements of *self* plus *object* added as last element. |
| excluding(object : T) : Sequence(T)                         | The sequence containing all elements of *self* apart from all occurrences of *object*. |
| asBag( ) : Bag(T)                                           | The Bag containing all the elements from *self*, including duplicates. |
| asSet( ) : Set(T)                                           | The Set containing all the elements from *self*, with duplicates removed. |
| asOrderedSet( ) : OrderedSet(T)                             | An OrderedSet that contains all the elements from *self*, in the same order, with duplicates removed. |

### Operations on OrderedSet(T)

| Operation                                                    | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| append(object : T) : OrderedSet(T)                           | The set of elements, consisting of all elements of *self* followed by *object*. |
| prepend(object : T) : OrderedSet(T)                          | The sequence consisting of *object*, followed by all elements in *self*. |
| insertAt(index : Integer, object : T) : OrderedSet(T)        | The Set consisting of *self* with *object* inserted at position *index*. |
| subOrderedSet(lower : Integer, upper : Integer) : OrderedSet(T) | The sub-set of *self* starting at index *lower*, up to and including the element at index *upper*; (1 <= *lower* <= *upper* <= size) |
| at(i : Integer) : T                                          | The *i*-th element of *self*; (1 <= *i* <= size)             |
| indexOf(object : T) : Integer                                | The index of *object* in the Sequence.                       |
| first( ) : T                                                 | The first element in *self*.                                 |
| last( ) : T                                                  | The last element in *self*.                                  |

### Operations Defined in OclAny

| Operation                            | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| = (object2 : OclAny) : Boolean       | True if *self* is the same object as *object2*.              |
| <> (object2 : OclAny) : Boolean      | True if *self* is a different object from *object2*.         |
| oclIsNew( ) : Boolean                | Only used in a postcondition. True if *self* was created during the operation execution. |
| oclAsType(t : OclType) : T           | Cast (type conversion) operation. Useful for downcast.       |
| oclIsTypeOf(t : OclType) : Boolean   | True if *self* is of type *t*.                               |
| oclIsKindOf(t : OclType) : Boolean   | True if *self* is of type *t* or a subtype of *t*.           |
| oclIsInState(s : OclState) : Boolean | True if *self* is in state *s*.                              |
| oclIsUndefined( ) : Boolean          | True if *self* is equal to *null* or *invalid*.              |
| oclIsInvalid( ) : Boolean            | True if *self* is equal to *invalid*.                        |
| allInstances( ) : Set(T)             | Static operation that returns all instances of a classifier. |

### Operations Defined in OclMessage

| Operation                   | Description                                                  |
| --------------------------- | ------------------------------------------------------------ |
| hasReturned( ) : Boolean    | True if type of template parameter is an operation call, and the called operation has return a value. |
| result( )                   | Returns the result of the called operation, if type of template parameter is an operation call, and the called operation has returned a value. |
| isSignalSent( ) : Boolean   | Returns true if the OclMessage represents the sending of a UML Signal. |
| isOperationCall() : Boolean | Returns true if the OclMessage represents the sending of a UML Operation call. |

