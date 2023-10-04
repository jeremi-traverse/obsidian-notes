In cpp, a reference is like an alias or another name for a variable that already exists and it's used via the Lvalue reference declarator : `&`

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

#### Rvalue reference declarator `&&`

Rvalue references support the implementation of move semantics. Move semantics enables you to write code that transfers resources (such as dynamically allocated memory) from on object to another. By doing so, we can increase the performance of our code simply by not making useless memory and copy allocations that are costly.

```cpp
// https://learn.microsoft.com/en-us/cpp/cpp/move-constructors-and-move-assignment-operators-cpp?view=msvc-170

class MemoryBlock
{
	public:
		// Simple constructor
		MemoryBlock(size_t length) 
		: _length(length)
		, _data(new int[length])
		{
		}
		
		~MemoryBlock()
		{
			if (_data != nullptr)
			{
				delete[] _data
			}
		}
		
		// Move constructor
		// A move constructor removes all values of its argument
		MemoryBlock(MemoryBlock&& other)
			: _data(nullptr)
			, _length(0)
		{
			// Assigning the class data members from the 
			// source object to the object being constructed
			_data = other._data;
			_length = other._length;

			// Assigning default values prevents the destructor from
			// freeing resources (i.e. memory) multiple times
			other._data = nullptr;
			other._length = 0;
		}
		
		MemoryBlock& operator=(MemoryBlock&& other)
		{
			if (this != &other)
			{
				delete[] _data;
	
				_data = other._data;
				_length = other._length;
	
				other._data = nullptr;
				other._length = 0;
			}
			return *this;
		}
		
	private:
		size_t _length;
		int* _data;
}
```