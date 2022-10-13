
# java 8 переход на java 11
2022-09-13 / 14:58

## Ссылки--java 8 переход на java 11
[[Java--core]]

---
## Мысли, пересказ--java 8 переход на java 11
### Java 9
#### коллекции
##### создание неизменяемой коллекции
```Java
List<Integer> integers = List.of(1, 2, 3);  
Set<String> strings = Set.of("one", "two", "three");  
Map<String, String> stringMap = Map.of( "k1", "v1", "k2", "v2");  
//        Вызовет исключение UnsupportedOperationException  
//        integers.add(2);
```

#### потоки
`takeWhile` - похоже на `.limit(Long max)` но здесь указывается предикат, в котором можно указать условие
- `dropWhile` - похож `.skip(Long n)`, но также используется предикат
- `iterate` - генерация последовательности. чем то похоже на list comprehension из питона
- `ofNullable` -  синтаксический сахар который позволяет не использовать тернарные операторы при изменении потока  
```Java
HashMap<String, String> stringHashMap = new HashMap<>();  
stringHashMap.put("one", "адын");  
stringHashMap.put("two", "два");  
System.out.println(stringHashMap.get("three"));  
//создаем список ключей, который отличается от ключей словаря  
List<String> keysList = List.of("one", "three");  
//получаем список значений словаря, если ключ есть в списке ключей  
List<String> valuesFromHashMap = keysList  
		.stream()  
		.flatMap(k -> Stream.ofNullable(stringHashMap.get(k)))  
		.collect(Collectors.toList());  
System.out.println(valuesFromHashMap); // [адын]
```

#### optional.ifPresentOrElse - принимает в себя 2 вызова: первый выполнится если есть значение,              второй если значение нет  
```Java
// create a Optional
Optional<Integer> op = Optional.of(9455);  
// print value  
System.out.println("Optional: " + op);  
// apply ifPresentOrElse  
op.ifPresentOrElse(  
		(value) -> { System.out.println(  
				"Value is present, its: "  
						+ value);  
		},  
		() -> { System.out.println(  
				"Value is empty");  
		}  
);
```

### Java 10
#### потоки: приведение к неизменяемой последовательности
```Java
List<Integer> integers = List.of(1, 2, 3, 4);  
Stream<Integer> integerStream = integers  
		.stream()  
		.filter(number -> number % 2 == 0);  

List<Integer> evenNumbersList = integerStream  
		.collect(Collectors.toUnmodifiableList());  
Set<Integer> evenNumbersSet = integerStream  
		.collect(Collectors.toUnmodifiableSet());  
//      также можно приводить к Map  
//                .collect(Collectors.toUnmodifiableMap())
```

#### var
var - это не является ключевым словом и не делает Java динамически типизированным языком.  
Однако с его помощью можно упростить написание кода.
Вот только есть куча нюансов
[Источник](https://habr.com/ru/post/438206/)   

##### Полезные применения       
```Java
// PREFER
var numbers = new int[5]; // inferred as array of int  
  
// значение при тернарных операторах
// PREFER
// inferred as Collection<Integer>
var code = containsDuplicates ? List.of(12, 1, 12) : Set.of(12, 1, 10);  
// inferred as Serializable
var code1 = intOrString ? 12112 : "12112";  


//using var in foreach  
List<String> orderList = List.of("Burger", "Coke", "Fries");  
for (var order : orderList) { // order type is inferred as String  
	System.out.println(order);  
}  
  
//краткая запись  
// вместо этого
MemoryCacheImageInputStream inputStream = new MemoryCacheImageInputStream();  
//используем краткую запись
var inputStream = new MemoryCacheImageInputStream(...);
```

### Java 11
#### новые методы в string API  
##### repeat
 ```Java
System.out.println("ha ".repeat(3)); //ha ha ha  
 ``` 

##### strip stripLeading stripTrailing
```Java
String stripStr = "    stripTestString          ";  
System.out.println("*" + stripStr.strip() + "*"); //*stripTestString*  
System.out.println("*" + stripStr.stripLeading() + "*"); //*stripTestString          *  
System.out.println("*" + stripStr.stripTrailing() + "*");
//*    stripTestString*  
```

##### isBlank
```java
System.out.println("".isBlank()); // true  
System.out.println(" ".isBlank()); // true  
System.out.println("\t".isBlank()); // true  
System.out.println("asdf".isBlank()); // false
```  

##### lines
```Java
"first line\nsecond line"
	.lines()
	.forEach(System.out::println);
//first line
// second line
```

#### Работа с файлами: writeString и readString
```Java
Path filePath = Files.writeString(
	Files.createTempFile("demo", ".txt"),
	"line 1\n line2"
);  
String fileContent = Files.readString(filePath);  
System.out.println("*" + fileContent + "*");
//*line 1
//line2*
```  
  
#### Collection.toArray()  
```Java
List<String> sampleList = Arrays.asList("Java", "Kotlin");  
String[] sampleArray = sampleList.toArray(String[]::new);
```  
  
#### Predicate.not  
```Java
List<String> sampleList1 = Arrays.asList(
	"Java", "\n \n", "Kotlin", " ");  
List withoutBlanks = sampleList
		.stream()  
		.filter(Predicate.not(String::isBlank))  
		.collect(Collectors.toList());  
System.out.println(withoutBlanks); // [Java, Kotlin]
```  
  
#### Local-Variable Syntax for Lambda
```Java
List<String> sampleList2 = Arrays.asList("Java", "Kotlin");  
String resultString = sampleList.stream()  
		.map((var x) -> x.toUpperCase())  
		.collect(Collectors.joining(", "));  
System.out.println(resultString); // JAVA, KOTLIN
```


#### работа с вложенными классами. кто является родителем, кто является ребенком
[тык](https://www.baeldung.com/java-11-new-features#7-nest-based-access-control)        

#### Optional.isEmpty()



---
## Вопросы--java 8 переход на java 11
