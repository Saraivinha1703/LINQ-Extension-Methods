# LINQ Extension Methods

All `Further Execution` LINQ methods, do not execute when they are called, they just execute when they need to turn into a List and passed to the client or be displayed. 

The `Immediate Execution` LINQ methods are executed when they are called for example the `Any`, `All` and `Contains` methods, are executed immediatly.

Most of the LINQ methods are `Further Execution`, the problem with not understanding it is the following: 
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Where(x => x > 2).Select(x => x.ToString());

var api1 = z.ToList();
var api2 = z.ToList();
```
The problem with this code is that the `z` variable did not get the result from the LINQ methods, they are executed when we call the `.ToList()` method when we pass the list to the "APIs". So we are executing the `Where` and `Select` methods twice, but a better way to solve this is the following:

```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Where(x => x > 2).Select(x => x.ToString()).ToList();

var api1 = z.ToList();
var api2 = z.ToList();
```

Using the `.ToList()` method at the end of the LINQ methods, will execute and pass a List to the `z` variable, which means that both API calls with the `ToList` method are unnecessary and will not execute the LINQ methods again, this way we execute everything just one time, but sometimes it is usefull to execute all the LINQ methods after something.

## Filtering

### Where (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Where(x => x > 2);
```
`var` is a enumerable of type `IEnumerable<int>`, the `Where` method is going to return the elements where the predicate returns true, so the `z` enumerable will have the following value: `[3, 4, 5]`, after being executed, for example using the `.ToList()` method.

### OfType (Further Execution)
```cs
IEnumerable<object> collection = [1, 2, "abc", 3, 4, 5];

var z = collection.OfType<int>();
```

`var` is a enumerable of type `IEnumerable<int>`, the `OfType` method is going to return the elements where the type of it is the type passed to the method, so the `z` enumerable will have the following value: `[1, 2, 3, 4, 5]`, after being executed, for example using the `.ToList()` method.

## Partitioning
### Skip (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Skip(3);
```
`var` is a enumerable of type `IEnumerable<int>`, the `Skip` method is going to return the elements after skiping the amount passed in the method, so the `z` enumerable will have the following value: `[4, 5]`, after being executed, for example using the `.ToList()` method.

### Take (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Take(3);
```
`var` is a enumerable of type `IEnumerable<int>`, the `Take` method is the opposite of the `Skip` and it is going to return the elements after taking the amount passed in the method, so the `z` enumerable will have the following value: `[1, 2, 3]`, after being executed, for example using the `.ToList()` method.

### SkipLast (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.SkipLast(3);
```
`var` is a enumerable of type `IEnumerable<int>`, the `SkipLast` method is going to take the whole collection and ignore the amount passed in the end of the array, so the `z` enumerable will have the following value: `[1, 2]`, after being executed, for example using the `.ToList()` method.

### TakeLast (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.TakeLast(3);
```
`var` is a enumerable of type `IEnumerable<int>`, the `TakeLast` method is going to skip the whole collection and take only the amount passed in the end of the array, so the `z` enumerable will have the following value: `[3, 4, 5]`, after being executed, for example using the `.ToList()` method.

### SkipWhile (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.SkipWhile(x => x < 2);
```
`var` is a enumerable of type `IEnumerable<int>`, the `SkipWhile` method is going to skip the whole collection while the predicate returns true for each element, so the `z` enumerable will have the following value: `[3, 4, 5]`, after being executed, for example using the `.ToList()` method.

<br/>

> **NOTE**: This method has nothing to do with the value of the number, if we had numbers that were  less than 2 after the five, they would be in the collection, for example:
> ```cs
> IEnumerable<int> collection = [1, 2, 3, 4, 5, 1, 1, 1];
> 
> var z = collection.SkipWhile(x => x < 2);
> ```
> `z` would have the following array: `[3, 4, 5, 1, 1, 1]`

### TakeWhile (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.TakeWhile(x => x < 2);
```
`var` is a enumerable of type `IEnumerable<int>`, the `TakeWhile` method is going to take the whole collection while the predicate returns true for each element, so the `z` enumerable will have the following value: `[1, 2]`, after being executed, for example using the `.ToList()` method.

<br/>

> **NOTE**: This method has nothing to do with the value of the number, if we had numbers that were  less than 2 after the five, they would be ignored, for example:
> ```cs
> IEnumerable<int> collection = [1, 2, 3, 4, 5, 1, 1, 1];
> 
> var z = collection.SkipWhile(x => x < 2);
> ```
> `z` would have the following array: `[1, 2]`

## Projection
### Select (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Select(x => x.ToString());
```

`var` is a enumerable of type `IEnumerable<string>`, the `Select` method is going to take the element and modify it however you want, so the `z` enumerable will have the following value: `["1", "2", "3", "4", "5"]`, after being executed, for example using the `.ToList()` method.

### SelectMany (Further Execution)
```cs
IEnumerable<List<int>> collection = [[1, 2, 3], [4, 5, 6]];

var z = collection.SelectMany(x => x);
```

`var` is a enumerable of type `IEnumerable<int>`, the `SelectMany` method is going to take an array and modify it however you want and transform this matrix into an array, so the `z` enumerable will have the following value: `[1, 2, 3, 4, 5, 6]`, after being executed, for example using the `.ToList()` method.

> **NOTE**: If you want to transform the values inside the matrix, use the select on the array inside, for example:
> ```cs
> IEnumerable<List<int>> collection = [[1, 2, 3], [4, 5, 6]];
> 
> var z = collection.SelectMany(x => x.Select(y => y.ToString()));
> ```
> `z` would have the following array: `["1", "2", "3", "4", "5", "6"]`

### Cast (Further Execution)
```cs
IEnumerable<object> collection = [1, 2, 3, 4, 5];

var z = collection.Cast<int>();
```
The `Cast` method will convert the enumerable type to the specified type.

### Chunck (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5, 6];

var z = collection.Chunk(3);
```

`var` is a enumerable of type `IEnumerable<int[]>`, the `Chunk` method is going transform the array into a matrix and the arrays inside will be the size specified in the method, so the `z` enumerable will have the following value: `[[1, 2, 3], [4, 5, 6]]`, after being executed, for example using the `.ToList()` method.

## Existence or Quantity Checks

### Any (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Any();
```


### All (Immediate Execution)


### Contains (Immediate Execution)

