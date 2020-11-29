# Темы для контрольной
## Оглавление
1. [Основы Swift](#Основы-Swift)
    * [Типы данных](#Типы-данных)
    * [Операторы](#Операторы)
    * [Циклы](#Циклы)
    * [Функции](#Функции)
    * [Замыкания](#Замыкания)
    * [Протоколы](#Протоколы)
    * [Наследование](#Наследование)
    * [Расширения протоколов](#Расширения-протоколов)
    * [Структуры](#Структуры)
    * [Классы](#Классы)
2. [UI & VC](#UI-&-VC)
3. [Коллекции](#Коллекции)
4. [Многопоточность](#Многопоточность)
5. [Работа с сетью](#Работа-с-сетью)
6. [Хранение данных](#Хранение-данных)
7. [Паттерны и шаблоны проектирования](#Паттерны-и-шаблоны-проектирования)

## Основы Swift
**Swift** — современный высокоуровневый строго типизированный объектно-ориентированный язык
для iOS и OS X. Он совместим с Objective-C, но привносит много идей и заимствований из других
современных языков: дженерики, функциональный стиль программирования, выведение типов.
Программы на нём рассчитаны на платформы OS X и iOS.
Swift позволяет избежать распространенных ошибок программирования, используя современные
шаблоны программирования:
* Переменные всегда инициализируются перед использованием.
* Индексы массива проверяются на наличие недопустимых ошибок.
* Целые числа проверяются на переполнение.
* Опционалы гарантируют, что значения nil обрабатываются явно.
* Память управляется автоматически.
* Обработка ошибок позволяет контролировать восстановление после непредвиденных сбоев.     

Код Swift компилируется и оптимизируется, чтобы максимально эффективно использовать
современное оборудование.             

[вернуться к оглавлению](#Оглавление)
### Типы данных   

**Объявление констант и переменных**

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
var x = 0.0, y = 0.0, z = 0.0
```

**Аннотация типов**


```swift
var welcomeMessage: String
```
Swift - язык со строгой типизацией.     
Swift всегда выбирает Double (вместо Float), когда выводит тип чисел с плавающей точкой:
``` swift
let pi = 3.14159
// pi выводится как тип Double
let anotherPi = 3 + 0.14159
// anotherPi тоже выводится как тип Double даже если есть целый литерал
```

**Простые типы**

* Целые числа: Int, UInt, Int8, Int16,… UInt64
* Числа с плавающей точкой: Double, Float
* Логический тип: Bool имеет значения true, false
``` swift
let i = 1
if i {
 // this example will not compile, and will report an error
}
```

**Строки и символы**

Строка - это серия символов, таких как `"hello, world"`. Строки Swift представлены типом String. Доступ к содержимому строки можно получить различными способами, в том числе в виде набора значений символов.  
Типы Swift String и Character обеспечивают быстрый Unicode-совместимый способ работы с текстом в вашем коде.    
Строковые литералы:
```swift
let singleLineString = "These are the same."
let multilineString = """
These are the same.
"""
```  

**Массивы**

Массив хранит значения того же типа в упорядоченном списке. Одно и то же значение может появляться в массиве несколько раз в разных позициях.   
Пример работы с массивами:
```swift
//Collections
var someInts = [Int] ()
var shoppingList: [String] = ["яйца", "молоко"]
shoppingList[0] = "перепелиные яйца"
shoppingList.insert("хлеб", at: 1)
shoppingList.append("пармезан")
print("for (index, item) in shoppingList.enumerated()")
for (index, value) in shoppingList.enumerated() { //для получения индексов используется enumerated()
 print("\(index + 1)" + ") " + value)
}
print("\nfor item in shoppingList")
for item in shoppingList {
 print(item)
}
```

**Множества**

Множество хранит различные значения одного и того же типа в коллекции без определенного порядка. Объекты должны быть хэшируемы, то есть подчиняться протоколу `Hashable`.   
Пример:
```swift
var set1 = Set<Character>()
set1.insert("A")
set1.insert("B")
set1.insert("C")
var set2: Set<Character> = ["C", "D", "E"]
print("union: \(set1.union(set2))")
print("subtracting: \(set1.subtracting(set2))")
print("intersection: \(set1.intersection(set2))")
print(“symmetricDifference: \(set1.symmetricDifference(set2))")
//union: ["B", "C", "D", "A", "E"]
//subtracting: ["B", "A"]
//intersection: ["C"]
//symmetricDifference: ["D", "E", “A", "B"]
```

**Словари**

В словаре хранятся ассоциации между ключами одного типа и значениями одного типа в коллекции без определенного порядка. Ключи должны быть Hashable.
```swift
var dict = Dictionary<String, String>()
dict.updateValue("торт", forKey: "десерт")
dict["основное блюдо"] = "медальон из говядины"
dict.merge(["напиток" : "квас"]) { (current, _) -> String in
 current
}
print(dict) //["десерт": "торт", "основное блюдо": "медальон из говядины", "напиток": “квас"]
dict["основное блюдо"] = "лазанья"
print(dict) //["десерт": "торт", "напиток": "квас", "основное блюдо": "лазанья"]
dict.removeValue(forKey: "десерт")
print(dict) //["основное блюдо": "лазанья", "напиток": "квас"]
for (key, value) in dict {
 print("\(key) - \(value)")
}
//основное блюдо - лазанья
//напиток - квас
for key in dict.keys {
 print(key)
}
//основное блюдо
//напиток
for key in dict.values {
 print(key)
}
//квас
//лазанья
```

[вернуться к оглавлению](#Оглавление)
### Операторы

[все операторы](https://developer.apple.com/documentation/swift/operator_declarations)     

**Оператор присваивания: = (не возвращает значения)**

```swift
var a = 1
var b = 2
if a = b { // Will produse "Use of '=' in a boolean context, did tou mean '=='?"
}
```

**Арифметические операторы: +, -, \*, /**  

В отличие от арифметических операторов в C и Objective-C, арифметические операторы Swift не допускают переполнения значений по умолчанию. Вы можете выбрать поведение переполнения, используя операторы переполнения Swift (например, a & + b):
```swift
var unsignedOverflow = UInt8.max
// unsignedOverflow equals 255, which is the maximum value a UInt8 can hold
unsignedOverflow = unsignedOverflow &+ 1
// unsignedOverflow is now equal to 0
```
Оператор сложения также поддерживается для конкатенации строк:
```swift
"hello, " + "world" // equals "hello, world”
```

**Оператор получения остатка: %**

```swift
-11 % 5 = -1
```

**Унарный минус: -**

```swift
let three = 3
let minusThree = -three
let plusThree = -minusThree // plusThree equals 3, or "minus minus three"
```
Унарный оператор минус (-) добавляется непосредственно перед значением, с которым он работает, без пробелов.        

**Унарный плюс: +**    

Унарный оператор плюс (+) просто возвращает значение, с которым он работает, без каких-либо изменений:
```swift
let minusSix = -6
let alsoMinusSix = +minusSix // alsoMinusSix equals -6
```

**Составные операторы присваивания: +=, -+, \*=, /=, … (не возвращают значение)**

```swift
var a = 1
a += 2 // a is now equal to 3
```

**Операторы сравнения: ==, <, >, <=, >=, !=, ===, ==**
```swift
(1, "zebra") < (2, "apple") // true because 1 is less than 2; "zebra" and "apple" are not compared
(3, "apple") < (3, "bird") // true because 3 is equal to 3, and "apple" is less than "bird"
(4, "dog") == (4, "dog") // true because 4 is equal to 4, and "dog" is equal to "dog"
("blue", -1) < ("purple", 1) // OK, evaluates to true
("blue", false) < ("purple", true) // Error because < can't compare Boolean values
```

**Операторы диапазона: m…n и m..<n**

```swift
for index in 1...5 {
 print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

**Односторонние диапазоны: n…, …n, ..<n**

```swift
let names = ["Anna", "Alex", "Brian", “Jack”]
for name in names[..<2] {
 print(name)
}
// Anna
// Alex
let range = ...5
range.contains(7) // false
range.contains(4) // true
range.contains(-1) // true
```

**Логические Операторы: !, &&, ||**

Логические операторы изменяют или объединяют значения логической логики true и false. Swift поддерживает три стандартных логических оператора в языках на основе C:      
> **Важно**     
> Логические операторы Swift && и || являются левоассоциативными, что означает, что составные выражения с несколькими логическими операторами сначала оценивают крайнее левое подвыражение.   

**Тернарные операторы: a ? b : c** - имеет возвращаемое значение  

**Сравнение множеств**

* Оператор «равно» (==), чтобы определить, содержат ли два множества все одинаковые значения.
* Метод `isSubset (of :)`, чтобы определить, содержатся ли все значения множества в указанном множестве.
* Метод `isSuperset (of :)`, чтобы определить, содержит ли множество все значения в указанном множестве.
* Методы `isStrictSubset (of :)` или `isStrictSuperset (of :)`, чтобы определить, является ли множества подмножеством или надмножеством, но не равным указанному множеству.
* Метод `isDisjoint (with :)`, чтобы определить, не имеют ли два множества общих значений.

**Конкатенация строк и символов**

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome now equals "hello there"
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
```

**Интерполяция строк**

```swift
let someInt = Int.random(in: 0...100)
print("some int from 0 to 100 is \(someInt)")
//some int from 0 to 100 is 8
```

**Подсчет символов**

```swift
var word = "cafe"
print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in cafe is 4"
word += "\u{301}" // COMBINING ACUTE ACCENT, U+0301
print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in café is 4"
```

**Вставка и удаление**

Чтобы вставить один символ в строку по указанному индексу, используйте метод `insert (_: at :)`, а для вставки содержимого другой строки по указанному индексу используйте метод `insert (contentsOf: at :)`.
Чтобы удалить один символ из строки по указанному индексу, используйте метод `remove (at :)`, а для удаления подстроки в указанном диапазоне используйте метод `removeSubrange (_ :)`:
```swift
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"
welcome.insert(contentsOf: " there", at:
welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"
```

**Сравнение строк**

Swift предоставляет три способа сравнения текстовых значений: равенство строк и символов, равенство префиксов и равенство суффиксов.
Равенство строк и символов проверяется с помощью оператора «равно» (==) и оператора «не равно» (! =):

```swift
// "Voulez-vous un café?" using LATIN SMALL LETTER E WITH ACUTE
let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"
// "Voulez-vous un café?" using LATIN SMALL LETTER E and COMBINING ACUTE ACCENT
let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"
if eAcuteQuestion == combinedEAcuteQuestion {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal”
```

**Префикс и суффикс**

Чтобы проверить, имеет ли строка определенный префикс или суффикс строки, вызовите методы `hasPrefix (_ :)` и `hasSuffix (_ :)` строки, оба из которых принимают один аргумент типа String и возвращают логическое значение.

[вернуться к оглавлению](#Оглавление)

### Циклы 

**Цикл For-in**   
Вы используете цикл `for-in` для итерации последовательности, такой как элементы в массиве, диапазоны чисел или символы в строке.
```swift
var array = [1, 2, 3, 4, 5]
for item in array {
    print("item = \(item)")
}
//item = 1
//item = 2
//item = 3
//item = 4
//item = 5
```

**Цикл while**

Цикл while выполняет набор операторов до тех пор, пока условие не станет ложным. Такие циклы лучше всего использовать, когда число итераций неизвестно до начала первой итерации.   
Swift предоставляет два вида циклов `while`:   
while оценивает свое состояние в начале каждого прохода цикла.   
`repeat-while` оценивает свое состояние в конце каждого прохода через цикл.   
Вот общая форма цикла `while`:   
```swift
while condition {
    statements
}
```
Вот общая форма цикла `repeat-while`:
```swift
repeat {
    statements
} while condition
```

**If**

В простейшем виде оператор `if` имеет единственное условие `if`. Он выполняет набор операторов, только если это условие истинно. Условные выражения в Swift работают как и в других C подобных языках:   
```swift
let a = 10
let b = 2
if a < b {
    print("\(a) < \(b)")
} else if a > b {
    print("\(a) > \(b)")
} else {
    print("\(a) == \(b)")
}
```

**switch**

Оператор `switch` рассматривает значение и сравнивает его с несколькими возможными шаблонами сопоставления. Затем он выполняет соответствующий блок кода на основе первого шаблона, который успешно соответствует. Оператор `switch` предоставляет альтернативу оператору if для ответа на несколько потенциальных состояний.   
В своей простейшей форме оператор `switch` сравнивает значение с одним или несколькими значениями одного
типа:
```swift
switch some value to consider {
case value 1:
 respond to value 1
case value 2, value 3:
 respond to value 2 or 3
default:
 otherwise
```

**Continue**

Оператор `continue` указывает циклу прекратить то, что он делает, и начать снова в начале следующей итерации цикла. Он говорит: «Я закончил с текущей итерацией цикла», не выходя из цикла вообще.
В следующем примере удаляются все гласные и пробелы из строчной строки для создания загадочной фразы-головоломки:
```swift
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
for character in puzzleInput {
    if charactersToRemove.contains(character) {
        continue
    }
    puzzleOutput.append(character)
}
print(puzzleOutput)
// Prints "grtmndsthnklk"
```

**Break**

Оператор break немедленно завершает выполнение всего оператора потока управления. Оператор `break` можно использовать внутри оператора `switch` или цикле, если вы хотите прекратить выполнение оператора `switch` или цикле раньше, чем в противном случае.


**Fallthrough**
В Swift операторы `switch` не попадают в нижнюю часть каждого дела и переходят к следующему.   
Привязка значений
```swift
let result = Result<String, Error>.success("Success")
var value = ""
switch result {
case .success(let string): //привязка значения
    value = string
    Fallthrough //провалиться в следующий кейз
default:
    print("value == " + value)
}
//value == Success
```

**Маркированные инструкции**

Метка пишется в той же строке, что и ключевое слово начала инструкции, которое следует после метки через двоеточие. Ниже приведен пример синтаксиса цикла `while`, хотя принцип работы маркера такой же со всеми инструкциями:
```swift
for1label: for i in 0...10 {
    var string = ""
    for j in 0...10 {
        string += "\(j)"
        if i == j {
        print(string)
            continue for1label
        }
    }
}
```

**Guard**

```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }
    print("Hello \(name)!")
    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }
    print("I hope the weather is nice in \(location).")
}
greet(person: ["name": "John"])
// Prints "Hello John!"
// Prints "I hope the weather is nice near you."
greet(person: ["name": "Jane", "location": "Cupertino"])
// Prints "Hello Jane!"
```

**Проверка доступности API**

```swift
if #available(platform name version, ..., *) {
    statements to execute if the APIs are available
} else {
    fallback statements to execute if the APIs are unavailable
}
```

[вернуться к оглавлению](#Оглавление)

### Функции

Функции - это отдельные фрагменты кода, которые выполняют определенную задачу. Вы даете функции имя, которое определяет, что она делает, и это имя используется для «вызова» функции для выполнения ее задачи, когда это необходимо.
```swift
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}
func sayHelloWorld() -> String {
    return "hello, world"
}
func greet(person: String) {
    print("Hello, \(person)!")
}
```

**Функции с несколькими возвращаемыми значениями**

Вы можете использовать тип кортежа в качестве возвращаемого типа для функции, которая возвращает несколько значений как часть одного составного возвращаемого значения. В приведенном ниже примере определяется функция minMax (array :), которая находит самые маленькие и самые большие числа в массиве значений Int:
```swift
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil }
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

**Функции с неявным возвратом**

Если все тело функции является одним выражением, функция неявно возвращает это выражение. Например, обе функции ниже имеют одинаковое поведение:
```swift
func greeting(for person: String) -> String {
 "Hello, " + person + "!"
}
print(greeting(for: "Dave"))
// Prints "Hello, Dave!"
func anotherGreeting(for person: String) -> String {
 return "Hello, " + person + "!"
}
print(anotherGreeting(for: "Dave"))
// Prints "Hello, Dave!"
```

**Вариативные параметры**

Параметр с переменным значением принимает ноль или более значений указанного типа. В приведенном ниже примере вычисляется среднее арифметическое для списка чисел любой длины:
```swift
func arithmeticMean(_ numbers: Double...) -> Double {
 var total: Double = 0
 for number in numbers {
 total += number
 }
 return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8.25, 18.75)
// returns 10.0, which is the arithmetic mean of these three numbers
```
> **Важно**   
> Функция может иметь не более одного вариативного параметра.

**Типы функций**

Каждая функция имеет определенный тип функции, состоящий из типов параметров и типа возврата функции.   
Например:
```swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
 return a + b
}
func multiplyTwoInts(_ a: Int, _ b: Int) -> Int {
 return a * b
}
```
Этот пример определяет две простые математические функции, называемые addTwoInts и multiplyTwoInts. Каждая из этих функций принимает два значения Int и возвращает значение Int, которое является результатом выполнения соответствующей математической операции.
Тип обеих этих функций `(Int, Int) -> Int`. Это можно прочитать как: «Функция, которая имеет два параметра, оба типа Int, и которая возвращает значение типа Int».

**Вложенные функции**
```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
 func stepForward(input: Int) -> Int { return input + 1 }
 func stepBackward(input: Int) -> Int { return input - 1 }
 return backward ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
 print("\(currentValue)... ")
 currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// -4...
// -3...
// -2...
// -1...
```

[вернуться к оглавлению](#Оглавление)

### Замыкания 
### Протоколы 
### Наследование
### Расширения протоколов
### Структуры
### Классы

# UI & VC
# Коллекции
# Многопоточность
# Работа с сетью
# Хранение данных
# Паттерны и шаблоны проектирования