# Unity Int Vectors
This library implements the Vector2i and Vector3i classes.
These are integer variants of Unity's Vector2 and Vector3 classes.

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
