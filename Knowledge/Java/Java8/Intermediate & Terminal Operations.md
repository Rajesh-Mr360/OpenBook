# Intermediate and Terminal operations in Java streams

Streams are designed to be functional, meaning that they allow you to perform operations on data in a way that is declarative and concise, without having to write loops or iterate over the data manually. This makes it easier to write code that is more readable, maintainable, and less error-prone.

In simple terms, you can think of a stream as a pipeline of data that you can manipulate and transform to get the output you want. Streams can be created from different data sources, such as **collections**, **arrays**, or **I/O channels**, and can be operated on using various operations provided by the Stream API.

==We can think of a stream like a pipeline that allows objects to flow through it. Intermediate operations are like valves or filters that can be used to modify the objects in the pipeline. You can use these operations to perform transformations on the objects, such as mapping them to a new value or filtering out certain objects based on some condition.== Other examples of intermediate operations include distinct(), sorted(), and `flatMap()`.

==Once you've made all the adjustments you want with intermediate operations, you can use a terminal operation to get a final result from the pipeline. Terminal operations are like the tap at the end of the pipeline that allows you to get the final output you want.== Some examples of terminal operations are toList(), forEach(), and reduce().


> [!NOTE] Internally
> It's important to understand that intermediate operations are not actually executed until a terminal operation is called. This is because Java streams use lazy evaluation, which means that they only evaluate the elements in the stream when necessary. This allows for more efficient processing of large collections of objects.

==Another important aspect of streams is that **they are designed to be used only once**. Once a terminal operation is called, the stream is consumed and cannot be used again. This is because streams are designed to be stateless and to operate on the data in a functional way.==

In summary, intermediate operations are like valves that allow you to modify the objects in the stream, while terminal operations are like the tap that allows you to get the final output you want. By mastering these concepts and using streams effectively, java folks can write more efficient and elegant code for processing collections of objects.


# Conclusion

- The main difference between intermediate and terminal operations is that intermediate operations return a stream as a result and terminal operations return non-stream values like primitive or object or collection or may not return anything.
- As intermediate operations return another stream as a result, they can be chained together to form a pipeline of operations. Terminal operations can not be chained together.
- Pipeline of operations may contain any number of intermediate operations, but there has to be only one terminal operation, that too at the end of pipeline.
- As the names suggest, intermediate operations doesn’t give end result. They just transform one stream to another stream. On the other hand, terminal operations give end result.
- **Intermediate Operations :** `map()`, `filter()`, `distinct()`, `sorted()`, `limit()`, `skip()`
- **Terminal Operations :** `forEach()`, `toArray()`, `reduce()`, `collect()`, `min()`, `max()`, `count()`, `anyMatch()`, `allMatch()`, `noneMatch()`, `findFirst()`, `findAny()`