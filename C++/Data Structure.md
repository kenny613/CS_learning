## Array
---
#### Array length issue
-  In C++, variable length arrays are not legal. G++ allows this as an "extension" (because C allows it), so in G++ (without being `-pedantic` about following the C++ standard), you can do:

```cpp
int n = 10;
double a[n]; // Legal in g++ (with extensions), illegal in proper C++
```
If you want a "variable length array" (better called a "dynamically sized array" in C++, since proper variable length arrays aren't allowed), you either have to dynamically allocate memory yourself:

```cpp
int n = 10;
double* a = new double[n]; // Don't forget to delete [] a; when you're done!
```

Or, better yet, use a standard container:

```cpp
int n = 10;
std::vector<double> a(n); // Don't forget to #include <vector>
```

If you still want a proper array, you can use a _constant_, not a _variable_, when creating it:

```cpp
const int n = 10;
double a[n]; // now valid, since n isn't a variable (it's a compile time constant)
```

Similarly, if you want to get the size from a function in C++11, you can use a `constexpr`:

```cpp
constexpr int n()
{
    return 10;
}

double a[n()]; // n() is a compile time constant expression
```