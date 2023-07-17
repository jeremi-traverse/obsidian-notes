A narrowing conversion happens when we cast a value from a given type to a smaller type. The result is that the smaller data type might not be able to hold some of the possible values.

```cpp
public Vector
{
	public:
		// list.size return size_t
		// sizeof(size_t) -> 8 bytes
		Vector(std::initializer_list<double> list) : size{list.size()}
	private:
		// sizeof(size) -> 4 bytes
		int size;
}
```