# Оглавление
- [О характеристиках языков программирования](#о-характеристиках-языков-программирования)
- [Типизация](#типизация)
- [Компилируемость и интерпретируемость](#компилируемость-и-интерпретируемость)
- [Однопоточность и многопоточность](#однопоточность-и-многопоточность)
- [Синхронность и асинхронность](#синхронность-и-асинхронность)
- [Кроссплатформенность и кроссбраузерность](#кроссплатформенность-и-кроссбраузерность)
- [Поддержка парадигм программирования](#поддержка-парадигм-программирования)
- [Синтаксис](#синтакс)

# Типизация
- [О системе типов и типизации](#о-системе-типов-и-типизации)
- [Статическая и динамическая типизация](#статическая-и-динамическая-типизация)
- [Слабая и сильная типизация](#слабая-и-сильная-типизация)
- [Явная и неявная типизация](#явная-и-неявная-типизация)

## О системе типов и типизации
- [Система типов](#система-типов)
- [Ошибка типа](#ошибка-типа)
- [Типизация и её классификация](#типизация-и-её-классификация)

### Система типов
*Рекомендуется почитать* о [**типах данных**](./DataTypes.md).

В *рамках изучения языков программирования* существует *понятие системы типов*.

**Система типов** (англ. type system) - такая *логическая система*, которая *связывает* некоторую *переменную* (*область памяти*, хранящую *данные*) с *определённым* **типом данных**. Эта *связь* означает, что после *установления типа переменная приобретает множество допустимых значений* и *ограниченный набор операций* над этими *значениями*. 

Например, для *переменной числового типа* могут быть *доступны операции инкремента* и *возведения в степень*: `x++`, `x^2`, а для *переменной строкового типа* - *операции поиска* и *получения подстроки*: `str.find(/* ... */)`, `str.substring(/* ... */)`.

### Ошибка типа

*Попытка выполнить операцию*, которая *выходит за пределы допустимых операций*, обычно *приводит* к **ошибке типа** (англ. type error). Например, *нельзя выполнить разность строк* или *поиск подстроки в числе*. 

Во многих языках программирования также нельзя выполнить бинарную операцию с операндами разных типов данных. Например, в Java нельзя сложить строку и число, при этом в JavaScript это допустимо, поскольку в этом случае происходит приведение операндов к одному типу.

### Типизация и её классификация

*Язык программирования*, *использующий систему типов*<!--  *обладающий* своей собственной *системой типов* -->, называется **типизированным языком** (англ.typed language).

В *широком смысле слова* под **типизацией** (англ typing) подразумевают *классификацию* по *типам*, конкретно в *рамках* изучения *языков программирования* под *типизацией* подразумевают то, каким образом система типов некоторого языка программирования обрабатывает типы данных в программе.

Например, *JavaScript* является *типизированным языком* и имеет *динамическую*, *слабую*, *неявную типизацию*.

## Статическая и динамическая типизация

*Типизированный язык* в определённый момент времени производит **проверку типа** (англ. type checking). 

<!-- о типобезопасности -->

*Проверка типа* может *производиться* во *время компиляции* (англ. compile time) или в *режиме реального времени* (англ. run-time), то есть *по ходу выполнения программы*.

При **стратической типизации** *типы устанавливаются* на *этапе компиляции*. К *моменту выполнения программы* они уже *установлены* и компилятор знает, где какой тип находится.

Пример языков со *статической типизацией*: *Java*, *C#*.
```java
/* Java */
public class Notes {
  public static void main(String []args){
    int number = 1; // числовой тип
    number = true; // error: incompatible types: boolean cannot be converted to int
  }
}
```

При **динамической типизации** *типы определяются во время работы программы*.

Пример языков с *динамической типизацией*: *Python*, *JavaScript*.
```js
/* JavaScript */
let a; // тип неизвестен
a = 1; // числовой тип
a = true; // логический тип
```

## Слабая и сильная типизация

При **слабой** (нестрогой) **типизации** *автоматически* выполняется множество *неявных преобразований типов* даже при условии *неоднозначности преобразования* или возможности *потери точности данных*.

Пример языка со *слабой типизацией*: *JavaScript*.
```js
/* JavaScript */
console.log(1 + [] + {} + 'notes'); // "1[object Object]notes"
console.log(1 - []); // 1
```

При **сильной** (строгой) **типизации** в выражениях *не разрешено смешивать различные типы*. *Автоматическое неявное преобразование не производится*. 

Пример языков с *сильной типизацией*: *Java*, *Python*.

Например, *нельзя сложить число* и *массив*.
```java
/* Java */
public class Notes {
  public static void main(String []args){
    int number = 17;
    int array[] = new int[3];
    System.out.println(number + array); // error: bad operand types for binary operator '+'
  }
}
```

## Явная и неявная типизация

При **явной типизации** *тип* новых *переменных*, *функции*, их *аргументов* и *возвращаемых* ими *значений* нужно задавать *явно*. 

Пример языков с *явной типизацией*: *C++*, *C#*.

```cpp
/* C++ */
int sum(int a, int b) {
    return a + b;
}
```

При **неявной типизации** эта *задание типов* производится *автоматически компиляторами* и *интерпретаторами*.

Пример языка с *неявной типизацией*: *JavaScript*.

```js
let a; // неизвестно, какого типа будет значение переменной
function fn (arg) { /* .. */ } // неизвестно, какого типа параметр функции и что она возвращает
```