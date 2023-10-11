# Лабораторна робота 5 : Принцип абстракції. Абстрактні класи та інтерфейси

## Завдання 1. Клас Animal

Даний наступний абстрактний клас

```java
abstract class Animal {

    private String name;

    public Animal(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    abstract String makeSound();
}
```

Створіть клас `Dog` як підклас `Animal` та реалізуйте метод `makeSound()`. Створіть клас `Cat` як підклас `Animal` та реалізуйте метод `makeSound()`. Створіть у методі `main()` об'єкти кожного з підкласів та викличте метод `makeSound()`.

## Завдання 2. Інтерфейс Movable

Напишіть вихідний код класу `Point`, який реалізує наступний інтерфейс

```java
interface Movable {
    void setX(double x);
    void setY(double y);
    double getX();
    double getY();

    void moveTo(double x, double y);
}
```

## Завдання 3. Клас Smartphone

Напишіть вихідний код класу `Smartphone`, який реалізує такі інтерфейси

```java
interface GPS {
    double[] getCoordinates();
}

interface Cellular {
    void makeCall();
    void receiveCall();
}
```

## Завдання 4. Інтерфейс Comparable

```java
class Car {

    private int price;
    private int year; // рік виготовлення
    private int horsePower;

    // Додайте конструктор з трьома аргументами

    // Додайте гетери та сетери
}
```

Зробіть так, щоб клас реалізовував інтерфейс `Comparable`. Напишіть вихідний код методу `compareTo()`. Логіка методу така:

- спочатку порівнюється ціна автомобілів, "більше" той автомобіль, у якого менша ціна;
- якщо ціни рівні, то порівнюється рік випуску автомобіля, "більше" той автомобіль, який менший за віком;
- якщо вік однаковий, то автомобілі порівнюються за кількістю кінських сил. "Більше" той автомобіль, у якого кінських сил більше.

> Не використовуйте типізований `Comparable`! Для порівняння використовуйте лише арифметичні оператори.

## Завдання 5. Додаток Draw

Скопіюйте та модифікуйте додаток `Draw` з лабораторної роботи №4 таким чином, щоб додаток використовував механізм абстрактних класів.

## Завдання 6. Додаток SortingList

В даному репозиторії присутній модуль `list`, який містить додаток для виведення списку студентів та дозволяє відсортувати їх за такими полями: ім'я, прізвище, середній бал.

В додатку вже реалізовано сортування студентів за ім'ям.

Завдання полягає в наступному:

- доробити додаток, щоб за натисканням на відповідні кнопки відбувалося сортування студентів за прізвищем та за середнім балом;
- **завдання на додаткові бали** - допрацюйте додаток таким чином, щоб при повторному натисканні на ту саму кнопку сортування здійснювалося зворотне сортування студентів. Тобто, при першому натисканні на кнопку "Сортування за ім'ям" студенти сортувалися у прямому порядку (за зростанням), а при повторному натисканні на цю ж кнопку, студенти сортувалися у зворотному порядку (за спаданням).

> Список студентів знаходиться в колекції `students`, для сортування необхідно викликати у колекції метод `sort()` і цей метод передати об'єкт компаратора.

### Що таке компаратор?

Базова операція для майже будь-якого сортування – порівняння двох елементів. Якщо ви сортуєте звичайні числа або рядки, порівняння відбувається елементарно за всім відомими правилами. Але що робити, якщо ви хочете відсортувати об'єкти, які можуть мати десятки полів різних типів?

Для цього існує так званий компаратор. Компаратор Java - це об'єкт класу, який реалізує інтерфейс `Comparator`. Інтерфейс визначає лише один метод `compare()`, який приймає на вхід два об'єкти типу `Object`. 

Якщо перший об'єкт "менше" - метод повертає від'ємне число (зазвичай це просто -1, але може бути і будь-яке інше від'ємне число), якщо перший об'єкт "більше" - метод повертає позитивне число (зазвичай це 1, але може бути будь-яке інше позитивне число), якщо об'єкти "рівні" - метод повертає 0.
Завдання програміста - прописати потрібну логіку порівняння та повернути -1/0/1 у тому чи іншому випадку.

Ви створюєте клас, вказуєте, що цей клас реалізує інтерфейс `Comparator` та у методі `compare()` описуєте логіку порівняння двох об'єктів. У випадку порівняння двох студентів по імені код компаратора виглядає наступним чином

```java
public class NameSorter implements Comparator {
    @Override
    public int compare(Object o1, Object o2) {
        if (o1 instanceof Student && o2 instanceof Student) {
            Student s1 = (Student) o1;
            Student s2 = (Student) o2;
            return s1.getName().compareTo(s2.getName());
        }
        return 0;
    }
}
```

Зверніть увагу, що спочатку ми повинні переконатися, що обидва об'єкти є об'єктами класу `Student`, після чого робимо низхідне перетворення.
У цьому випадку ми порівнюємо два поля name у двох об'єктів класу `Student`. Так як це тип `String`, нам не потрібно порівнювати рядки «вручну», ми просто можемо скористатися методом `compareTo()`, який є у будь-якого об'єкта класу `String`.
