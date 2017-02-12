# Unity Int Vectors
This library provides integer vectors, Vector2i and Vector3i.
These are integer variants of Unity's Vector2 and Vector3 classes and implement all functionality that you would expect.
 
### A familiar interface
Vector2i and Vector3i use the same interface as Vector2 and Vector3.
Practically every function that is defined for Vector2/Vector3 is also defined for Vector2i/Vector3i.
    
### Usefull predifined values
All the predifined values from Vector2/Vector3 are also defined for Vector2i/Vector3i:
  
  * zero (Vector2i and Vector3i)
  * one (Vector2i and Vector3i)
  * up (Vector2i and Vector3i)
  * down (Vector2i and Vector3i)
  * left (Vector2i and Vector3i)
  * right (Vector2i and Vector3i)
  * forward (only Vector3i)
  * back (only Vector3i)
  
### All operators are implemented
All mathematical and equality operations are supported:
```
  var minus_two = -2 * vector3i.one;
  var treasure_location = 5 * vector2i.right + 3 * vector2i.up;
  var b = -vector2i.one == vector2i.one - minus_two;
```
  
### Effortless integration
No need to rewrite all your exisiting code.
Just call any function accepting Vector2/Vector3 and pass it a Vector2i/Vector3i!
Of course this also works with any third party library you are using or are planning to use.
Implicit conversion from int to float types does all the work for you.

Implicit conversion only happens from int to float and not the other way around, so this won't accidentally cause rounding errors:
```
   public static Vector3 f(Vector3 x) { ... }
   public static Vector3i g(Vector3i x) { ... }
   
   ...
   
   Vector3 a;
   Vector3i b;
   
   ...
   
   Vector3  r0 = f(b);            // OK
   Vector3i r1 = f(b);            // Compile Error - potential bug by accidentally casting float to int
   Vector3i r2 = (Vector3i)f(r2); // OK - make it explicit if it really is what you want to do
   Vector3  r3 = g(a);            // OK
   Vector3i r4 = g(b);            // Compile Error - potential bug by accidentally casting float to int
   vector3i r5 = g((Vector3i)b);  // OK -  make it explicit if it really is what you want to do
```

### Semantically correct code
Of course, it is possible to use float Vectors and to store integer values.
However, this is very error prone.
To make sure that a float vector always contains integer coordinates, you either have to round the vector after every mutation or make sure that every mutation results in new integer value coordinates.

By using the correct type, Vector2i or Vector3i, you move this responsibility from the programmer to the compiler.

An additional benefit of Vector2i and Vector3i is that the type immediately makes clear to the reader, that int values are expected. Otherwise you would have to make this clear in the documentation of the code.

### RectLoops and CubeLoops
The library also adds new control structures, that make it easier to loop over values of vectors.

```
// Where you would normally write
for(int x = 0; x < 10; ++x) {
  for(int y = 2; y < 12; ++y) {
    MyFunction(new Vector(x, y));
  }
}

// you can write
RectLoop(
  new Vector2i(0, 2),
  new Vector2i(10, 12),
  MyFunction
);


// Where you would normally write
for(int x = 0; x < 10; ++x) {
  for(int y = 2; y < 12; ++y) {
    for(int z = -4; z < 8; ++z) {
      MyFunction(new Vector(x, y, z));
    }
  }
}

// you can write
CubeLoop(
  new Vector3i(0, 2, -4), 
  new Vector3i(10, 12, 8), 
  MyFunction
);
````
