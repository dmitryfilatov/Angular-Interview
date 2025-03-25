## <a name="type"></a>Что такое псевдоним типа?
Псевдоним типа — это способ определить новое имя для типа, чтобы сделать код более понятным. Он создается с использованием ключевого слова type и существует в коде только до момента компиляции. Псевдонимы могут быть использованы для определения примитивных типов, объединений, пересечений. По сути он служит только для проверки типов в коде.

Вот пример псевдонима типа:

```typescript
type UserID = string;

type User = {
  id: UserID;
  name: string;
  age: number;
  email?: string; // необязательное поле
};
```
<br/>

## <a name="interface_type"></a>В чём отличие interface от type?

Интерфейсы допускают дополнение объявлений, а псевдонимы типов — нет. Дополнение объявлений позволяет добавлять свойства в интерфейс даже после того, как он был объявлен:

```typescript
 interface Person {
  name: string;
 }
 interface Person {
  age: number;
 }
 // Person сейчас { name: string; age: number; }
```
Если изменить интерфейс на псевдоним типа это выдаст ошибку:

```typescript
 type Person {
  name: string;
 }
 type Person {
 //   ^-- Duplicate identifier 'FormData'.(2300)
  age: number;
 }
``` 

С другой стороны, тип может объединять другие типы, а интерфейс - нет:

```typescript
  type AorB = 'a' | 'b';
``` 
Примечание: interface и type существуют только до момента компиляции, и после компиляции будут удалены.
<br/>

## <a name="class_type"></a>В чём отличие class от type?

class:
- Определяет шаблон для создания объектов.
- Поддерживает наследование и инкапсуляцию.
- Может содержать методы и свойства.

type:
- Определяет псевдоним для типов данных.
- Не поддерживает создание экземпляров.
- Используется для проверки типов, не компилируется в JavaScript.

Примечание: type может описывать объекты, содержащие стрелочные функции или обычные функции в качестве полей. Это не означает, что type добавляет функциональность в самом объекте, но он может определять сигнатуры функций в объекте для проверки типов.
<br/>

## <a name="type_intersection"></a>Что такое пересечение типов?

Это способ комбинирования нескольких типов в один. Объект пересечения должен удовлетворять всем объединённым типам. Оператор & используется для создания пересечений.

Пример пересечения типов:

```typescript
type Person = {
  name: string;
  age: number;
};

type Employee = {
  employeeId: number;
  department: string;
};

type EmployeeDetails = Person & Employee;

// Объект employee должен содержать свойства всех объединённых типов.
const employee: EmployeeDetails = {
  name: "Alice",
  age: 30,
  employeeId: 12345,
  department: "Engineering",
};
```
<br/>

## <a name="override_function"></a>Есть ли в TypeScript перегрузка функций?

Да, TypeScript в отличие от JavaScript** поддерживает перегрузку функций с помощью нескольких объявлений разных сигнатур перед одной-единственной реализацией, внутри которой делаются проверки переданных типов.

```typescript
function greet(name: string): string;
function greet(names: string[]): string;
function greet(nameOrNames: string | string[]): string {
  if (typeof nameOrNames === 'string') {
    return `Hello, ${nameOrNames}!`;
  } else {
    return `Hello, ${nameOrNames.join(' and ')}!`;
  }
}

console.log(greet('Alice')); // "Hello, Alice!"
console.log(greet(['Alice', 'Bob'])); // "Hello, Alice and Bob!"
``` 
** JavaScript переопределяет функцию с тем же именем её последней реализацией
<br/>

## <a name="this"></a>Как в TypeScript определить на какой тип указывает this внутри функции?

 Можно явно указать тип this внутри функции, используя аннотацию перед списком параметров функции.

 ```typescript
class MyClass {
  value: number;

  constructor(value: number) {
    this.value = value;
  }

  // Определение типа this
  increment(this: MyClass, amount: number): void {
    this.value += amount;
  }
}

const obj = new MyClass(10);
obj.increment(5);
console.log(obj.value); // 15
```
Примечание: параметр с this удаляется после компиляции.
<br/>

## <a name="annotationthis"></a>Когда нужно и когда не нужно применять аннотацию типов?

Не нужно, когда компилятор сам способен вывести тип:

```typescript
let aValue = 3; // aValue: number
``` 
желательно при получении значения из функции, чтобы убедиться, что функция возвращает нужный тип.
```typescript
const me: Person = createPerson();
``` 
И крайне важно применять а.т. к параметрам сигнатуры функции, чтобы компилятор проверил типы в момент передачи параметров.
<br/>

## <a name="struct_typing"></a>Что такое структурная типизация?

Это когда типы совместимы по членам, но не по имени.

```typescript
 type Person = {
  name: string;
  age: number;
 };
 type User = {
  name: string;
  age: number;
  id: number;
 };
 //функция может принимать User, если в теле её используются только члены, идентичные Person
 function printPerson(person: Person) {
  console.log(person.name, person.age);
 }
``` 
<br/>

## <a name="unknown"></a>Что такое тип unknown и для чего он используется?

Это тип, который представляет собой значение, тип которого неизвестен. В отличие от any, который позволяет выполнять любые операции с переменной, unknown требует проверки типа прежде чем использовать значение.

```typescript
let value: unknown;

value = "Hello";
// console.log(value.toUpperCase()); // Ошибка: Object is of type 'unknown'.

if (typeof value === "string") {
    console.log(value.toUpperCase()); // Теперь это безопасно
}
``` 
Используется для переноса данных, которые имеют неизвестный тип. Использование unknown позволяет сначала проверить данные, прежде чем с ними работать.
<br/>

## <a name="rest_types"></a>Что такое остаточные типы?

Они были введены в JavaScript в стандарте ECMAScript 2015 (ES6) для массивов и в ECMAScript 2018 (ES9) для объектов. 
Используются для управления остаточными параметрами в функциях и для работы с массивами и объектами. Они позволяют собирать несколько оставшихся аргументов функции в единый параметр или объединять свойства объекта в один объект.

в функциях:
```typescript
function sum(...numbers: number[]): number {
    return numbers.reduce((acc, num) => acc + num, 0);
}

console.log(sum(1, 2, 3)); // 6
``` 
в объектах:
```typescript
const person = { name: 'Alice', age: 25, job: 'Developer' };
const { name, ...rest } = person;

console.log(name); // Alice
console.log(rest); // { age: 25, job: 'Developer' }
``` 
в массивах:
```typescript
const [first, second, ...rest] = [1, 2, 3, 4, 5];

console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4, 5]
``` 
<br/>

## <a name="spread"></a>Что такое оператор распространения?

Cинтаксическая конструкция в JavaScript и TypeScript, которая представляет собой многоточие .... Она позволяет развернуть элементы массива или свойства объекта в местах, где ожидается набор значений. 

```typescript
const numbers = [1, 2, 3];
//создает поверхностную копию массива
const copyOfNumbers = [...numbers];

const array1 = [1, 2];
const array2 = [3, 4];
//соединяет несколько массивов в один:
const combined = [...array1, ...array2]; // [1, 2, 3, 4]

const person = { name: 'Alice', age: 30 };
//создает поверхностную копию объекта
const copyOfPerson = { ...person };

const defaults = { theme: 'light', showNotifications: true };
const userSettings = { theme: 'dark' };
//Объединяет объекты, где свойства последующих объектов могут перезаписывать свойства предыдущих.
const settings = { ...defaults, ...userSettings }; // { theme: 'dark', showNotifications: true }
``` 
<br/>

## <a name="namespaces"></a>Чем пространство имён типов отличается от пространства имён значений?

Пространство имён типов:

- Содержит определение типов, таких как интерфейсы, типы, перечисления
- Типы используются на этапе компиляции для проверки корректности кода.
- Пространство имён типов удаляется после компиляции.

Пространство имён значений:

- Содержит определение переменных, функций, классов, перечислений (enum в их значимой части) и т.д.
- Значения существуют в итоговом JavaScript-коде и исполняются на этапе выполнения.
- Всё, что находится в этом пространстве имён, превращается в реальные объекты или функции в скомпилированном коде.

Пример для перечисления (enum), охватывающий оба пространства:

```typescript
enum Direction {
  Up,    // Значение
  Down,  // Значение
  Left,  // Значение
  Right  // Значение
}

function move(direction: Direction) { // Здесь Direction используется как тип
  if (direction === Direction.Up) {  // Здесь Direction используется как значение
    console.log("Moving up");
  }
}
``` 
<br/>

## <a name="symbol"></a>Для чего используется тип symbol?

Для представления уникальных и неизменяемых примитивных значений.
 
Особенности:
- каждый символ уникален. Даже если два символа создаются с одинаковым описанием, они не считаются равными.
- могут служить ключами для свойств объектов.
- свойства, чьи ключи являются символами, не показываются в обычных итерациях по объекту, например, в for...in циклах или Object.keys(), что позволяет более "приватное" хранение данных.
- не сериализуются в стандартные форматы, такие как JSON.

Пример использования:

```typescript
const uniqueId = Symbol("uniqueId");

const user = {
  name: "Alice",
  [uniqueId]: 12345, // символ используется как ключ
};

console.log(user[uniqueId]); // 12345
``` 
<br/>