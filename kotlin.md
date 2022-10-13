# Kotlin
2022-07-29 / 14:30

## Ссылки--Kotlin
[[язык программирования]]


---
## Мысли,пересказ--Kotlin
### Модификаторы и операторы
`val` - модификатор "только для чтения". Похоже на `final` в Java
`const` - почти тоже самое что `val` но применяется для примитивов или иммутабельных значений
`var` - обычное значение. можно изменять
То есть `val` - value, как литерал (пятерка, стань двойкой. Нет, так не получится (с))
`var` - variable, значение или же классическая переменная. Можно изменять

`Unit` - тип возврата аля `void` в java. Но скорее всего с каким то нюансами.
как тип возврата Unit указывать не обязательно

`vararg`  - указывается перед аргументом функции, чтобы указать что это последовательность, в которой содержится переменное количество элементов

### Варианты объявления переменной
```Kotlin
val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred
val c: Int  // Type required when no initializer is provided
c = 3       // deferred assignment
```

### Ветвления (условия и т.п.)
`if` 
`else`
`when` - что то типа `switch` но это другая реализация, а именно pattern matching (как в Rust и Python)

### Циклы
#### For
```Kotlin
//Однострочный цикл (привет Python)
for (item in collection) print(item)

// Java-like foreach
for (item: Int in ints) {
	// ...
}

// диапазон от 1 до 3 включительно
for (i in 1..3) {
    println(i)
}

// диапазон от 1 до 3 НЕ включительно
for (i in 1 until 3) {
    println(i)
}

//downTo для отрицательного шага
for (i in 6 downTo 0 step 2) {
    println(i)
}

// работа с индексами последовательности.
//Аля for i in range(len(somelist)) в python
for (i in array.indices) {
    println(array[i])
}


//Использование ключа и значения. Аля enumerate в python
for ((index, value) in array.withIndex()) {
    println("the element at $index is $value")
}
```
##### for в диапазоне символов
```Kotlin
for (c in 'a'..'d') {        // 1
    print(c)
}
print(" ")

for (c in 'z' downTo 's' step 2) { // 2
    print(c)
}
print(" ")
```

#### While
`while` `do-while`



### Типы данных
`is` - проверка типа данных.
```Kotlin
if (someVal is String) {/* ...*/}

//Эквивалент Java
if (someVal isinstaceof String) {/*...*/}
```
#### Примитивы
Всё очень похоже на Java. Правда есть примитивы без отрицательных чисел
##### Строки
есть аналог многострочной строки из python

Строка форматирования
```Kotlin
val s = "abc"
println("$s.length is ${s.length}") // prints "abc.length is 3"
```
Использование строки форматирования как шаблон слияния (join)
```Kotlin

    fun accum(s: String): String {
        var index = 0
        return s
                .chunked(1)
                .joinToString("-") {
                    "${it.toUpperCase()}${it.repeat(index++).toLowerCase()}"
                }
    }
```

`.ifBlank() { default_value }`
`.substringAfter`

#### Массивы
`emptyArray()`
`arrayOF()` 
Есть спец. версии массивов, содержащие примивы
`ByteArray` `ShortArray` `IntArray` и др.



### Функциональное программирование
#### Ф-ии высшего порядка

#### Лямбда-функции
```Kotlin
val upperCase1: (String) -> String = { str: String -> str.uppercase() } 

val upperCase2: (String) -> String = { str -> str.uppercase() }        

val upperCase3 = { str: String -> str.uppercase() }                   

//Ошибка. Тип всё таки надо указать или в переменной или в теле лямбды                       
// val upperCase4 = { str -> str.uppercase() }  

val upperCase5: (String) -> String = { it.uppercase() }              

val upperCase6: (String) -> String = String::uppercase              

```

#### JS-like прикручивание полей и функций в уже готовую структуру
https://play.kotlinlang.org/byExample/04_functional/03_extensionFunctions

### Структуры данных
#### List
`listOf()`  - как tuple в python
`mutableListOf()` - как list в python

#### Set
`setOf()`
`mutableSetOf()`

#### Map
`mapOf()`
`mutableMapOf()`

##### Получение значения по ключу
someMap["key"] - выдаст значение если ключ `key` есть в структуре, если нет - вернет `null`
someMap.getValue("key") - значение или же исключение `NoSuchElementException`

#### взаимодействие со структурой (как в JS)
`.filter` - есть доп варианты. см. доку
`.map`

`.any` `.all` `.none` - принимает предикат, возвращает boolean

`find` `findLast`

`first` `last` `firstOrNull` `lastOrNull` - также может принимать предикат(лямбду для фильтрации последовательности перед тем как взять значение)

`count` - также принимает предикат

`getOrElse` - получить значение по ключу или индексу, если нет такого ключа вернуть значение по умолчанию
```Kotlin
val list = listOf(0, 10, 20)
println(list.getOrElse(1) { 42 })    // 1
println(list.getOrElse(10) { 42 })   // 2




val map = mutableMapOf<String, Int?>()
println(map.getOrElse("x") { 1 })       // 1

map["x"] = 3
println(map.getOrElse("x") { 1 })       // 2

map["x"] = null
println(map.getOrElse("x") { 1 })       // 3
```

`.take(n: Int)` - взять первых `n` элементов
`.drop(n)` - скинуть первых `n` элементов

### Разное
`TODO()` - для кода который не имеет реализации. Будет вызвано исключение







---
## Вопросы--Kotlin
[[qq/Kotlin/sumBy]]
[[qq/Kotlin/String chunked]]
[[qq/Kotlin/eachCount]]
[[qq/Kotlin/дата классы]]


[[qq/Kotlin/Pair и Pairs]]
[[qq/Kotlin/переменная it]]
[[qq/Kotlin/null safe]]
[[qq/Kotlin/object и companion object]]
[[qq/Kotlin/тройное равно]]
[[qq/Kotlin/any и outAny]]
[[qq/Kotlin/operator]]
[[qq/Kotlin/Collections - associateBy и groupBy]]
[[qq/Kotlin/фп и два двоеточия]]


[[qq/Kotlin/scope functions]]
[[qq/Kotlin/infix functions]]
