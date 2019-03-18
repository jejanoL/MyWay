---
layout: post
title:  "Hashtable and Dictionary"
date:   2019-03-13 
categories: DataStructures
tags: [C#, HashTable, DataStructures]
---


A dictionary is a collection in which each element is a key/value pair. Dictionaries
are most commonly used for lookups and sorted lists.

Key-and-value pair collection types:
Implement the System.Collections.IDictionary interface
* System.Collections.Hashtable class
* System.Collections.Generic.Dictionary<TKey,TValue> generic class
 (Also implements the IDictionary<TKey,TValue> generic interface)
* System.Collections.Concurrent.ConcurrentDictionary<TKey,TValue> generic class

In general, you should use generic collections. The original collection classes are largely considered deprecated by developers and by Microsoft itself. In fact they indicate that for the most part you should always favor the generic or concurrent collections, and only use the original collections when you are dealing with legacy .NET code.

<!-- more -->

## Properties and Methods 

Only listed some important ones. 

### Properties

* **Count**

	Gets the total number of elements exists in the Dictionary<TKey,TValue>.

* **IsReadOnly**
	
	Returns a boolean indicating whether the Dictionary<TKey,TValue> is read-only.
* **Item**	
	
	Gets or sets the element with the specified key in the Dictionary<TKey,TValue>.
* **Keys**	
	
	Returns collection of keys of Dictionary<TKey,TValue>.
* **Values**

	Returns collection of values in Dictionary<TKey,TValue>.

### Methods

* **Add**	
	
	Adds an item to the Dictionary collection.
* **Add**	
	
	Add key-value pairs in Dictionary<TKey, TValue> collection.
* **Remove**	
	
	Removes the first occurance of specified item from the Dictionary<TKey, TValue>.
* **Remove**	
	
	Removes the element with the specified key.
* **ContainsKey**	
	
	Checks whether the specified key exists in Dictionary<TKey, TValue>.
* **ContainsValue**	
	
	Checks whether the specified value exists in Dictionary<TKey, TValue>.
* **Clear**	
	
	Removes all the elements from Dictionary<TKey, TValue>.
* **TryGetValue**	
	
	Returns true and assigns the value with specified key, if key does not exists then return false.

### Related Methods

#### ToDictionary

LINQ. Extension methods can be used with Dictionary. We use the ToDictionary method. This is an extension method on IEnumerable. It places keys and values into a new Dictionary.

The example uses ToDictionary, from System.Linq, on a string array. It creates a lookup table for the strings.

```      
	string[] values = new string[]
	{
		"One",
		"Two"
	};
	// Create Dictionary with ToDictionary.
	// ... Specify a key creation method, and a value creation method.
	var result = values.ToDictionary(item => item, item => true);
	foreach (var pair in result)
	{
		Console.WriteLine("RESULT PAIR: {0}, {1}", pair.Key, pair.Value);
	}
````

### Code Samples

* Create a dictionary.

```
	var myDict = new Dictionary<int, string>
	{
	    {1, "test1"},
	    {2, "test2"},
	    {3, "test3"}
	};
```

* Iterate over the collection of all the KeyValuePairs in the dictionary.

```
	foreach (KeyValuePair<int, string> kvp in myDict)
	{ 
	    Console.WriteLine("Key = {0}, Value = {1}", kvp.Key, kvp.Value); 
	} 
```

* Add a value associated to a key.

```
	myDict.Add(4, "test4"); // adds "test4" as number 4
```

* Update the value associated with a key.

```
	myDict[1] = "test11"; // number 1 is now "test11"
```

* Get the associated value of a key.

```
	var myValue = myDict[2]; // myValue = "test2"
```

* Check whether Dictionary contains the key.

```
	if (myDict.ContainsKey(5))
	{
		string value = myDict[5];
		Console.WriteLine(value);
	}
```

* Lookup for the key, then returns the value if it finds the key.

```
	if (myDict.TryGetValue(4, out test)) // Returns true.
	{
	Console.WriteLine(test); // This is the value for 4, "test4".
	}
```

* Get the associated value of a key.

```
	var myValue = myDict[2]; // myValue = "test2"
```

* Remove a key/value pair.

```
	myDict.Remove(3); // number 3 (test3) has been removed from the dictionary
```

* Get the associated value of a key.

```
	var myValue = myDict[2]; // myValue = "test2"
```


## Comparisons

### Choosing a Collection

| Use for | Generic collection options | Non-generic collection options | Thread-safe or immutable collection options |
| ------- | :----------  | :----------- | :--------   |
| Store items as key/value pairs for quick look-up by key | Dictionary<TKey,TValue>  | Hashtable (A collection of key/value pairs that are organized based on the hash code of the key.)   | ConcurrentDictionary<TKey,TValue>, ReadOnlyDictionary<TKey,TValue>, ImmutableDictionary<TKey,TValue> |


### Collection Efficiency


| Type    | Internal structure | Ordering    | Contiguous Storage? | Direct Access      | Lookup Efficiency | Manipulate Efficiency | Notes       |
| ------- | :----------        | :---------- | :----------         | :----------        | :------------       |:----------            | :---------- |
| Dictionary <K,V> | Hashtable | Unsorted    |Yes                  | Via Key            | O(1)          | O(1)| Best for high performance lookups |
| Hashtable        | Hashtable | Unsorted    |Yes                  | Via Key            | O(1)          | O(1)| Associative, unordered collection of key-value pairs of objects |
| OrderedDictionary| Hashtable + array | Unsorted |Not Sure            | Via Index/Key  | O(1)          | O(1)| there’s no generic version |
| ListDictionary   | Linked list | Unsorted  |Not Sure             | Via Key            | O(n)          | O(n)| Extremely slow with large lists. Its only real “claim to fame” is its efficiency with very small lists (fewer than 10 items)|
| SortedDictionary <K,V> | Red/black tree| Sorted | No	           | Via Key            | O(log n)     | O(log n)| Compromise of Dictionary speed and ordering, uses binary search tree |
| SortedList <K,V> | 2xArray   | Sorted      | Yes	               | Via Index?Index    | O(log n)     | O(n)| Very similar to SortedDictionary, except tree is implemented in an array, so has faster lookup on preloaded data, but slower loads, favor the generic collection SortedList<T> instead. |

## Leetcode List


## References

*  [Microsoft](https://docs.microsoft.com/en-us/dotnet/standard/collections/) Microsoft Collections and Data Structures
* [blogs](http://geekswithblogs.net/BlackRabbitCoder/archive/2011/06/16/c.net-fundamentals-choosing-the-right-collection-class.aspx) Comparison across collections 
 