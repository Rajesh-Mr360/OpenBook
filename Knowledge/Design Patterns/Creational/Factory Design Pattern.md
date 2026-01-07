The **Factory Design Pattern** is a creational design pattern that let's you create objects without exposing the actual creation logic. Instead creating objects directly using `new` keyword, we simply ask the **Factory** to create object for us and Factory will do it for us.

There are three key components in Factory design pattern:

1. **Product Interface :** This is the interface (or abstract class) that the factory class returns. It consist of a common set of methods that **every concrete product must implement**, ensuring they all follow the same structure and behavior.
2. **Concrete Products :** These are the actual classes that implement the product interface. Each class provides its own specific behavior, but still follows the common structure. The factory creates and returns these products based on what the client needs.
3. **Factory Class :** This class is used by clients to create product objects. It holds all the creation logic, and its main purpose is to return the right product instance based on what the client asks for.

![700](images/FactoryDesignPattern.png)

## Why this matters for "Clean Code"

Without a Factory, your code ends up with "If-Else" hell:
```Java
// BAD: This code is hard to maintain and repeat
if (fileType.equals("JSON")) {
    JsonParser parser = new JsonParser();
    parser.parse(data);
} else if (fileType.equals("XML")) {
    XmlParser parser = new XmlParser();
    parser.parse(data);
}
```

With a Factory, it becomes a single, clean line:

```Java
// GOOD: Clean, readable, and decoupled
ParserFactory.getParser(fileType).parse(data);
```

And the factory class holds the actual creation logic:

```Java
public class ParserFactory {

    // The creation logic is encapsulated here
    public static LogParser getParser(String fileType) {
        if ("JSON".equalsIgnoreCase(fileType)) {
            return new JsonLogParser();
        } else if ("XML".equalsIgnoreCase(fileType)) {
            return new XmlLogParser();
        } else if ("CSV".equalsIgnoreCase(fileType)) {
            return new CsvLogParser();
        }
        throw new IllegalArgumentException("Unsupported file type: " + fileType);
    }
}
```


# The "Registry" (Map-based) Factory

Once you get to 20 or 30 different parsers, a giant `if-else` block becomes hard to read. In professional Java EE (like Spring or Micronaut), we use a **Map-based Registry**.

This is how the "Pro" version looks:

```Java
public class ParserFactory {
    // A registry of all available parsers
    private static final Map<String, LogParser> registry = new HashMap<>();

    // Static block or a 'register' method to fill the map
    static {
        registry.put("JSON", new JsonLogParser());
        registry.put("XML", new XmlLogParser());
        registry.put("CSV", new CsvLogParser());
    }

    public static LogParser getParser(String fileType) {
        LogParser parser = registry.get(fileType.toUpperCase());
        if (parser == null) {
            throw new RuntimeException("No parser found for: " + fileType);
        }
        return parser;
    }
}
```

**Why is this even better ?**
**O(1) Lookup:** No more checking 100 `if` conditions; it looks it up instantly in the Map.



