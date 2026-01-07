Sorting is a fundamental operation in any programming language for organizing data in a specific order. In Java, the build in sorting methods provides efficient ways to sort primitive data types, making it easier to organize the data. For instance, you can quickly sort an array of Integers of list of Strings using `Arrays.sort()` and `Collections.sort()`.

However, when it comes to sorting custom objects such as instances of user-defined classes or database entities, the built-in sorting methods won’t work out of the box. These methods don’t know how to determine the order of such objects. This is where Java’s `Comparable` and `Comparator` interfaces come into play, allowing developers to implement custom mechanisms for ordering data. Below is how we can use these interfaces to implement a custom sorting mechanism.
## Comparable
A `Comparable` is an interface that consist of only one method named `compareTo()`, which returns an integer as a result. Our user defined class must implement this method to provide default sorting order. 

The `compareTo()` method follows a simple convention:
- It returns a negative integer if the calling object is less than the object being compared.
- zero if the calling object is equal to the object being compared.
- positive integer if the calling object is greater than the object being compared.

Once implementing the Comparable interface, objects can be sorted using the `Arrays.sort()` or `Collections.sort()` methods, which internally use the `compareTo()` method to determine the order.

Here’s an example implementation of the Comparable interface for a custom class called `Person`:\

```java ln:false title:"Person.java"
@Getter
@Setter
@AllArgsConstructor
public class Person implements Comparable<Person> {
	private String name;
	private int age;
	
	@Override
	public int compareTo(Person otherPerson) {
		//Change in order of compare() method arguments 
		//helps to acheive ASC/DESC order of elements :) 
		return Integer.compare(this.age, otherPerson.age);  
	}
}
```

```java ln:false title:"PersonSortingExample.java"
public class PersonSortingExample {  
	public static void main(String[] args) {  
		
		Person[] people = {  
			new Person("Alice", 25),  
			new Person("Bob", 30),  
			new Person("Charlie", 22)  
		};  
		
		Arrays.sort(people);  
		for (Person person : people) {  
			System.out.println(person.getName() + ": " + person.getAge() + " years old");  
		}  
	}  
}
```

```:output ln:false
Charlie: 22 years old  
Alice: 25 years old  
Bob: 30 years old
```


## Comparator
The Comparator interface provides an alternative way to sort objects. This interface allows you to create separate comparison logic without modifying the original class.

The Comparator interface defines a single method called `compare()`, which takes two objects as input and returns an integer value indicating the comparison result. The `compare()` method follows the same convention as the `compareTo()` method:

- It returns a negative integer if the first object is less than the second object.
- It returns zero if the first object is equal to the second object.
- It returns a positive integer if the first object is greater than the second object.

The Comparator interface provides flexibility by allowing multiple comparison rules for the same class, based on different attributes or criteria.

Here’s an example implementation of the Comparator interface for the `Person` class, comparing two persons based on their names:

```Java ln:false
@Getter
@Setter
@AllArgConstructor
public class Person {
	private String name;
	private Integer age;
	private String country;
}

public class Main {
	public static void main(String[] args) {
		List<Person> personList = new ArrayList<>();  
		personList.add(new Person(3, "Ram", 26));  
		personList.add(new Person(1, "Chinna", 23));  
		personList.add(new Person(7, "Dhikonda", 27));  
		personList.add(new Person(5, "Dev", 22));  
		
		//Collections.sort(personList, new NameComparator())
		personList.sort(new NameComparator());  
		  
		for(Person p : personList) {  
		    System.out.println(p);  
		}
	}
}

class NameComparator implements Comparator<Person> {  
    @Override  
    public int compare(Person p1, Person p2) {  
        return p1.getName().compareToIgnoreCase(p2.getName());  
    }  
}
```

If we do not provide a comparator in the sort method and also do not override the `compareTo()` method, which sorts based on the name, an error will occur, stating that it did not find any method to perform the sorting:

If we want to use our custom comparator and sort the objects based on the name, it is necessary to provide an instance of the comparator class along with the list of objects we wish to sort:

`{Java} Collections.sort(people, new PersonNameComparator());`