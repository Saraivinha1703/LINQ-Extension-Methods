# LINQ Extension Methods (Language Integrated Query)

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

### Chunk (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3, 4, 5, 6];

var z = collection.Chunk(3);
```

`var` is a enumerable of type `IEnumerable<int[]>`, the `Chunk` method is going transform the array into a matrix and the arrays inside will be the size specified in the method, so the `z` enumerable will have the following value: `[[1, 2, 3], [4, 5, 6]]`, after being executed, for example using the `.ToList()` method.

## Existence or Quantity Checks

### Any (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var y = collection.Any(x => x < 2);
var z = collection.Any();
```
`var` is a boolean, the first `Any` method will check if there is any element inside the array that is less than 2, if the predicate is true, it will return true and wont continue to process the array. The second method is used only to check if there is anything inside the array, returns false if it is empty. 

### All (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.All(x > 4);
```
`var` is a boolean, the `All` method will check if all the elements inside the array are greater than 4, if the predicate is false, it will return false and wont continue to process the array. 

### Contains (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Contains(4);
```

`var` is a boolean, the `Contains` method will check if the passed element is inside the array, returns true when it is found.

## Sequence Manipulation
### Append (Further Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Append(6);
```
`var` is a enumerable of type `IEnumerable<int>`, the `Append` method is used to add values at the end of the array, so the `z` enumerable will have the following value: `[1, 2, 3, 4, 5, 6]`, after being executed, for example using the `.ToList()` method.


### Prepend (Further Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Prepend(0);
```
`var` is a enumerable of type `IEnumerable<int>`, the `Append` method is used to add values at the beggining of the array, so the `z` enumerable will have the following value: `[0, 1, 2, 3, 4, 5]`, after being executed, for example using the `.ToList()` method.

## Aggregation Methods
### Count (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Count();
```
`var` is an integer type, the `Count` method counts how many elements exists inside an array.

### TryGetNonEnumeratedCount (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.TryGetNonEnumeratedCount(out var count);
```
`var` is a boolean type, the `TryGetNonEnumeratedCount` method counts how many elements exists inside an array and outputs the result and return a boolean, false if it is a enumerable that was not computed yet, for example, if there was a `Where` or `Select` or any other `Further Execution` it would return false, but if it is a list it would return true.

### Max (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Max(x => x * -1);
```
`var` is an integer type, the `Max` method will execute the calculation and return the highest value, so the `z` variable will have the following value: `-1`, and that's because we are multiplying all the values with -1 and -1 is the highest number between -2, -3, etc.

### MaxBy (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.MaxBy(x => x * -1);
```
`var` is an integer type, the `MaxBy` method will execute the calculation and return the actual element that was used in the calculation where the result was the highest value, so the `z` variable will have the following value: `1`, and that's because we are multiplying all the values with -1 and -1 is the highest number between -2, -3, etc. the element that corresponds to -1 is 1, and that's what the method returns.

### Min (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Min(x => x * -1);
```
`var` is an integer type, the `Min` method will execute the calculation and return the lowest value, so the `z` variable will have the following value: `-5`, and that's because we are multiplying all the values with -1 and -5 is the lowest number between -1, -2, etc.

### MinBy (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.MinBy(x => x * -1);
```
`var` is an integer type, the `MinBy` method will execute the calculation and return the actual element that was used in the calculation where the result was the lowest value, so the `z` variable will have the following value: `5`, and that's because we are multiplying all the values with -1 and -5 is the lowest number between -1, -2, etc. the element that corresponds to -5 is 5, and that's what the method returns.

### Sum (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Sum();
```
`var` is an integer type, the `Sum` method will sum all the elements, this method only works to number types like `int` or `double`, if you want to use other type you have to cast or pass a number value. The `z` variable will have the following value: `15`.

### Average (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Average();
```
`var` is an integer type, the `Average` method will sum all the elements and divide by their amount (in this case we have five elements), this method only works to number types like `int` or `double`, if you want to use other type you have to cast or pass a number value. The `z` variable will have the following value: `3`.

### Aggregate (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Aggregate((x, y) => x + y);
```
`var` is an integer type, the `Aggregate` method will take the first and second element, for the next iteration `x` will be the result of the first iteration and `y` will be the next element on the array. The `z` variable will have the following value: `15`.
You can also change the first iteration with a default value, for example if we wanted to sum 10 in the first iteration it would be like this:

```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Aggregate(10, (x, y) => x + y);
```

The result would be `25`.
And we can also do something at the end with the last iteration, for example:

```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Aggregate(10, (x, y) => x + y, x => x / 5);
```
This would divide the result of all the iterations, which is 25, by 5 and the `z` variable would have its value seted to `5`.

### LongCount (Immediate Execution)
Its the same as the `Count` method but returns a `long` type.

## Element Operators

### First (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.First();
```

`var` is an integer type, the `First` method will return the first element of the array, if the array does not have any elements an `InvalidOperationException` will be thrown.

### FirstOrDefault (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.FirstOrDefault();
```

`var` is an integer type, the `FirstOrDefault` method will return the first element of the array, if the array does not have any elements it will return the default value for your specific type, in this case it is an integer so it would return a 0, but you can also specify your default value passing it to the method.

### Single (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Single();
```
`var` is an integer type, the `Single` method expects that the array have only one element and return this element if it is the only one, but if there is more than one element an exception will be thrown. 

### SingleOrDefault (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.SingleOrDefault();
```
`var` is an integer type, the `SingleOrDefault` method expects that the array have only one element and return this element if it is the only one, but if there is more than one element an exception will be thrown, if there is no elements the default will be returned. 

### Last (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.Last();
```

`var` is an integer type, the `Last` method will return the last element of the array, if the array does not have any elements an `InvalidOperationException` will be thrown.

### LastOrDefault (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.LastOrDefault();
```

`var` is an integer type, the `LastOrDefault` method will return the last element of the array, if the array does not have any elements it will return the default value for your specific type, in this case it is an integer so it would return a 0, but you can also specify your default value passing it to the method.

### ElementAt (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.ElementAt(1);
```
`var` is an integer type, the `ElementAt` method takes an index value and returns the element at that index, if the index does not exist in the array an exception will be thrown.

### ElementAtOrDefault (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.ElementAtOrDefault(1);
```

`var` is an integer type, the `ElementAt` method takes an index value and returns the element at that index, if the index does not exist in the array the default value will be returned.

### DefaultIfEmpty (Further Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.DefaultIfEmpty();
```

`var` is of type `IEnumerable<int>`, the `DefaultIfEmpty` method will add a default value to the collection if it is empty.

## Conversion Methods
### ToArray (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.ToArray();
```
`var` is of type `int[]`, the `ToArray` method transforms the enumerable into an array and all the LINQ queries that were declared previously are computed.

### ToList (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.ToList();
```
`var` is of type `List<int>`, the `ToList` method transforms the enumerable into a list and all the LINQ queries that were declared previously are computed.

### ToDictionary (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.ToDictionary(key => key, value => value);
```
`var` is of type `Dictionary<int, int>`, the `ToDictionary` method transforms the enumerable into a dictionary and expects a key and a value to be specified and all the LINQ queries that were declared previously are computed.

### ToHashSet (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.ToHashSet();
```
`var` is of type `HashSet<int>`, the `ToHashSet` method transforms the enumerable into a `HashSet` and all the LINQ queries that were declared previously are computed.

### ToLookup (Immediate Execution)
```cs 
IEnumerable<int> collection = [1, 2, 3, 4, 5];

var z = collection.ToLookup(x => x);
```
`var` is of type `ILookup<int, int>`, the `ToLookup` method transforms the enumerable into a collection of groups, in this case each group would be identified by the number and all the LINQ queries that were declared previously are computed.

> **NOTE**: A more interesting way to use the `ToLookup` method, would be like this:
> ```cs
> IEnumerable<Person> collection = [
>     new("A", 20), 
>     new("B", 23), 
>     new("C", 23)
> ];
> 
> var z = collection.ToLookup(x => x.Age);
> 
> record Person(string Name, int Age);
> ```
> In this case `z` would be of type `ILookup<int, Person>` and the groups would be divided according to the parameter passed in the `ToLookup` method, which means that we would have a group identified by `20` with only the person with name `A` and other group identified by `23` which would have two persons with the names `B` and `C`.

## Generation Methods
### AsEnumerable (Further Execution)
```cs 
List<int> collection = [1, 2, 3, 4, 5];

var z = collection.AsEnumerable();
```
`var` is of type `IEnumerable<int>`, the `AsEnumerable` method is used to cast a collection to a enumerable.

### AsQueryable (Further Execution)
```cs 
List<int> collection = [1, 2, 3, 4, 5];

var z = collection.AsQueryable();
```
`var` is of type `IQueryable<int>`, the `AsQueryable` method is used to cast a collection to a queryable collection.

### Range (Immediate Execution)
```cs
IEnumerable<int> collection = Enumerable.Range(3, 4);
```

The `Range` method receives a starting number and counts from this number including it, until it reaches the count that you passed, in this case, we would have a collection with number from 3 to 6. This method only works for number types.

### Repeat (Immediate Execution)
```cs
IEnumerable<int> collection = Enumerable.Repeat(3, 4);
```

The `Repeat` method receives a number and repeats it the amount of times that you passed, in this case, we would have a collection like this: `[3, 3, 3, 3]`.

### Empty (Immediate Execution)
```cs
IEnumerable<int> collection = Enumerable.Empty<int>();
```

The `Empty` method is a static method, which means if we use a lot of collections and use this method, all collections will be referencing to the same empty collection.

## Set Operations
### Distinct (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 1, 3, 2, 3, 2, 1]; 

var z = collection.Distinct();
```
The `z` is of type `IEnumerable<int>`, the `Distinct` method will remove all the elements that are the same and return only the elements that are different. In this case, the `z` enumerable would have the following value: `[1, 2 ,3]`.

### DistinctBy (Further Execution)
```cs
IEnumerable<Person> collection = [
    new("A", 20),
    new("B", 22),
    new("C", 22),
    new("D", 23),
    new("E", 20),
]; 

var z = collection.DistinctBy(x => x.Age);

record Person(string Name, int Age);
```

The `z` is of type `IEnumerable<Person>`, the `Distinct` method will remove all the elements that have the same age and return only the elements that are different. In this case, the `z` enumerable would have a collection with the persons with the names `A`, `B` and `D`.

### Union (Further Execution)
```cs
IEnumerable<int> collection1 = [1, 2, 3];
IEnumerable<int> collection2 = [2, 3, 4];

var z = collection1.Union(collection2);
```
the `z` is of type `IEnumerable<int>`, the `Union` method will ignore the values that overlap and concatenate the values that are different, so the `z` collection would have the following value: `[1, 2, 3, 4]`.

### Intersect (Further Execution)
```cs
IEnumerable<int> collection1 = [1, 2, 3];
IEnumerable<int> collection2 = [2, 3, 4];

var z = collection1.Intersect(collection2);
```
the `z` is of type `IEnumerable<int>`, the `Intersect` method will ignore the values that are specific in each collection and take only the values that overlap, so the `z` collection would have the following value: `[2, 3]`.


### Except (Further Execution)
```cs
IEnumerable<int> collection1 = [1, 2, 3];
IEnumerable<int> collection2 = [2, 3, 4];

var z = collection1.Except(collection2);
```

the `z` is of type `IEnumerable<int>`, the `Except` method will ignore the values that are the same and unique on the collection passed to the method and take only unique values in the first collection, in other words, we are basically subtracting `collection2` from `collection1`, so the `z` collection would have the following value: `[1]`.

### UnionBy (Further Execution)
Similar to the `Union` method, but you can use it with objects and pass a specific property to base the union.

### IntersectBy (Further Execution)
Similar to the `Intersect` method, but you can use it with objects and pass a specific property to base the intersections.

### ExceptBy (Further Execution)
Similar to the `Except` method, but you can use it with objects and pass a specific property to base the exceptions.

### SequenceEqual (Immediate Execution)
```cs
IEnumerable<int> collection1 = [1, 2, 3];
IEnumerable<int> collection2 = [1, 2, 4];

var z = collection1.SequenceEqual(collection2);
```
the `z` variable is type boolean, the `SequenceEqual` method checks if a collection is equal to the other one comparing its values. In this case `z` would be false.
 
## Joining & Grouping
### Zip (Further Execution)
```cs
IEnumerable<int> collection1 = [1, 2, 3, 4];
IEnumerable<string> collection2 = ["a", "b", "c"];

var z = collection1.Zip(collection2);
```
the `z` variable is of type `IEnumerable<ValueTuple<int, string>>`, the `Zip` method will run through the lists and put the values in each position together, if there are more values in one list than the other, those values will be ignored. In this case `z` would have the value: `[{"Item1": 1, "Item2": "a"}, {"Item1": 2, "Item2": "b"}, {"Item1": 3, "Item2": "c"}]`

> **NOTE**: We can use more than two collections

### Join (Further Execution)
```cs
IEnumerable<Person> collection1 = [
    new(0, "A", 20), 
    new(1, "B", 22), 
    new(2, "C", 22), 
    new(3, "D", 23)
];
IEnumerable<Product> collection2 = [
    new(0, 0, "Glasses"),
    new(1, 2, "Shirt"),
    new(2, 1, "Gloves"),
    new(3, 3, "Shoes"),
    new(4, 0, "Chain"),
    new(5, 0, "Watch"),
    new(6, 2, "Shorts"),
    ];

var z = collection1.Join(
    collection2,
    person => person.Id,
    product => product.PersonId,
    (person, product) => $"{person.Name} bought {product.Name}");

record Person(int Id, string Name, int Age);
record Product(int Id, int PersonId, string Name);
```

`z` is a `IEnumerable<string>`, the `Join` method will take a collection, the keys to match the items and give the matching elements, then you can do whatever you want with the elements and return something, in this case `z` is getting a list of strings saying the products that which person bought, in this case the list should look something like this: `["A bought Glasses", "C bought Shirt", "B bought Gloves", "D bought Shoes", "A bought Chain", "A bought Watch", "C bought Shorts"]` 

### GroupJoin (Further Execution)
This method is very similar to the `Join` method, the difference is that instead of getting each product per person, you would have a list of products that were bought for that person.

```cs
var z = collection1.Join(
    collection2,
    person => person.Id,
    product => product.PersonId,
    (person, products) => $"{person.Name} bought {string.Join(',', products)}");
```
The value of `z` would be something like: `["A bought Product { Id = 0, PersonId = 0, Name = "Glasses" },Product { Id = 4, PersonId = 0, Name = "Chain" },Product { Id = 5, PersonId = 0, Name = "Watch" }", "B bought Product { Id = 2, PersonId = 1, Name = "Gloves" }", "C bought Product { Id = 1, PersonId = 2, Name = "Shirt" },Product { Id = 6, PersonId = 2, Name = "Shorts" }", "D bought Product { Id = 3, PersonId = 3, Name = "Shoes" }"]`.

### Concat (Further Execution)
```cs
IEnumerable<int> collection1 = [1, 2, 3];
IEnumerable<int> collection2 = [4, 5, 6];

var z = collection1.Concat(collection2);
```

the `z` is type `IEnumerable<int>`, the `Concat` method will only append the array passed to the method in the end of the array, so the result would be: `[1, 2, 3, 4, 5, 6]`.

### GroupBy (Further Execution)
Similar to the `ToLookup` method, but it is not executed immediatly and returns a different type, but you can make groups passing a property to base the groups, like in the `ToLookup` example.

## Sorting
### Order (Further Execution)
```cs
IEnumerable<int> collection = [3, 1, 2];

var z = collection.Order();
```
`z` is a `IEnumerable<int>` type, this is a simple example and the `Order` method will organize the array to be in a ascending order, it should have the following value: `[1, 2, 3]`

### OrderDescending (Further Execution)
```cs
IEnumerable<int> collection = [3, 1, 2];

var z = collection.OrderDescending();
```
`z` is a `IEnumerable<int>` type, this is a simple example and the `OrderDescending` method will organize the array to be in a descending order, it should have the following value: `[3, 2, 1]`

### OrderBy (Further Execution)
Does the same as the `Order` method, but you can pass a specific property from a object to order based on that, for example the age of persons, in this case, it would give an enumerable with the youngest to the oldest person.

### OrderByDescending (Further Execution)
Does the same as the `OrderDescending` method, but you can pass a specific property from a object to order based on that, for example the age of persons, in this case, it would give an enumerable with the oldest to the youngest person.

### ThenBy (Further Execution)
```cs
IEnumerable<Person> collection = [
    new("A", 20),
    new("B", 19),
    new("A", 22)
];

var z = collection.OrderBy(x => x.Name).ThenBy(x => x.Age);

record Person(string Name, int Age);
```
`z` is a `IEnumerable<Person>` type, the `ThenBy` method, will apply the order respecting the previous order by the name, this sorting should result in the following value: `[{ Name: "A", Age: 20 }, { Name: "A", Age: 22 }, { Name: "B", Age: 19 }]`

### ThenByDescending (Further Execution)
```cs
IEnumerable<Person> collection = [
    new("A", 20),
    new("B", 19),
    new("A", 22)
];

var z = collection.OrderBy(x => x.Name).ThenByDescending(x => x.Age);

record Person(string Name, int Age);
```
`z` is a `IEnumerable<Person>` type, the `ThenByDescending` method, will apply the order respecting the previous order by the name, this sorting should result in the following value: `[{ Name: "A", Age: 22 }, { Name: "A", Age: 20 }, { Name: "B", Age: 19 }]`

### Reverse (Further Execution)
```cs
IEnumerable<int> collection = [1, 2, 3];

var z = collection.Reverse();
```

`z` is of type `IEnumerable<int>`, the `Reverse` method inverts the order of a collection, this should result on the following array: `[3, 2, 1]`.

## PLINQ (Parallel LINQ)
Parallel LINQ have access to all the LINQ methods but runs them concurrently.

### AsParallel
```cs
using System.Diagnostics;

var stopwatch = Stopwatch.StartNew();

var collection = Enumerable.Range(0, 10)
    .AsParallel()
    .Select(HeavyComputation);

//this line is just used to run the Select method
foreach(var _ in collection);

stopwatch.Stop();
Console.WriteLine(stopwatch.ElapsedMilliseconds);

int HeavyComputation(int n) 
{
    for(int i = 0; i < 100_000_000; i++)
    {
        n += i;
    }

    return n;
}
```

This enumerable have only 10 items and we are computing data that without the `AsParallel` method would take around 2.5 seconds, but with this method the `Select` runs for each item in parallel and take the execution time to something around 0.2 seconds.

### WithDegreeOfParallelism


### ParallelEnumerable.Range


### ParallelEnumerable.Repeat


### ParallelEnumerable.Empty


### AsSequential


### AsOrdered


### AsUnordered


### WithCancellation


### WithMergeOptions


### WithExecutionMode


### ForAll

