In cpp, a reference is like an alias or another name for a variable that already exists

```cpp
int i = 0; // original value, to be referenced
int& r_i = i; // alias to i, the reference
int* p_i = &i // pointer that points to i

// Adding to i with a reference
void add_to_int(int& r)
{
	r+=5;
}

// Adding to i with a pointer
void add_to_int(int* r)
{
	*r+=5;
}

cout << i << "\n"; // 0
cout << ri << "\n"; // 0

add_to_int(r_i);

cout << i << "\n"; // 5
cout << ri << "\n"; // 5

add_to_int(p_i);

cout << i << "\n"; // 10
cout << ri << "\n"; // 10
```

You might think that a reference is exactly like a pointer ? They are, but not exactly

```cpp
int& illegal_reference = NULL // Can't create a reference to null
int& legal_reference = int_that_exists // Always to a variable that exists

int& illegal_reference = int_that_exists
illegal_reference = antoher_int_that_exists // Can't rereference another variable

int& ref = i;
int& illegal_ref = &i+4 // Cannot do math on references

int& legal_reference = x;
int&& illegal_reference = &legal_reference // Cannot have a reference of a reference
```

Under the hood, the assembly for both pointers and references are exactly the same. All the protection that reference gives us are applied at compile time.

Usage of references adds more safety to the code since they are basically pointers with restrictions.