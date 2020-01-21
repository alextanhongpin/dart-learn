# dart-learn
Learning Dart, and Flutter


## Installation

```bash
$ brew tap dart-lang/dart
$ brew install dart

$ pub global activate stagehand
```

## Creating a new project with stagehand

```bash
$ mkdir cli
$ cd cli
$ stagehand console-full

# Get dependencies
$ pub get

# Run the app
$ dart bin/main.dart

# Run test
$ pub run test
```

## Basics

```dart
void main() {
  print("hello world");
  
  for (var i = 0; i < 5; i++) {
    print(i);
  }
  
  int myAge = 100;
  String myName = 'john doe';
  var myGender = 'm';
  const isMarried = true;
  print("$myAge, $myName, $myGender, $isMarried");
  
  var one = int.parse("1");
  print(one.isOdd);
  try {
    var two = int.parse("two");  
  } catch (error) {
    print(error.message);
  }
  
  var dbl = double.parse("1.234");
  print(dbl);
  String multiline = """
    This is a multiline string.
    Haha
  """;
  print(multiline);
  
  List fruits = ["apple", "banana", "durian"];
  print(fruits);
  for (var fruit in fruits) {
    print(fruit);
  }
  print(fruits.first);
  print(fruits.last);
  
  
  var books = {'Harry Potter', 'Lord of the Rings'};
  print(books.lookup('Harry Potter'));
  print(books.lookup('this'));
  
  var myMap = {}; 
  print(myMap.isEmpty);
  
  
  int firstNum;
  int secondNum = 100;
  int thirdNum = 200;
  firstNum ??= secondNum;
  thirdNum ??= secondNum;
  print(firstNum);
  print(thirdNum);
}
```

## Basics
```dart
void main() {
  bool isTrue = true;
  String str = "hello world";
  print(isTrue is bool);
  print(isTrue is! bool);
  print(str is String);
  print(str is! String);
  
  for (var i = 0; i < 10; i++) {
    print(i);
  }
  
  outerloop: for(var i = 0; i < 10; i++) {
    innerloop: for (var j = 0; j < 10; j++) {
      print(i + j);
      if (i == 5 && j == 5) {
        print("breaking outerloop: $i and $j"); 
        break outerloop;
      }
    }
  }
  
  var points = 100;
  switch (points) {
    case 10:
      print('got 10 points');
      break;
    case 100:
      print('got 100 points');
      break;
    default:
      print('others');
  }
}
```

## Classes

```dart
class Car {
  int model = 123;
  String name = "Proton";
  bool isOn = true;
  
  bool turnOn(bool turnOn) {
    isOn = turnOn;
    return isOn;
  }
  
  bool isTurnedOn() {
    return isOn;
  }
}

void main() {
  var car = new Car();
  print(car.isTurnedOn());
  car.turnOn(false);
  print(car.isTurnedOn());
  print(car.name);
}
```

```dart
class Bear {
  int numberOfFish;
  int hoursOfSleep;
//   Bear(this.numberOfFish, this.hoursOfSleep);
  
  Bear(int numberOfFish, int hoursOfSleep) {
    this.numberOfFish = numberOfFish;
    this.hoursOfSleep = hoursOfSleep;
  }
  
  int get hours => hoursOfSleep;
  set hours(int n) => hoursOfSleep = n;
  
  int eatFish() => numberOfFish;
  int sleepAfterEatingFish() => hoursOfSleep;
  int weightGained() => numberOfFish * hoursOfSleep;
}


void main() {
  var bear = new Bear(10, 5);
  
  print(bear);
  print(bear.eatFish());
  print(bear.sleepAfterEatingFish());
  print(bear.weightGained());

  bear.hours = 100;
  print(bear.hours);
}
```

## Default and Optional Parameters

```dart
void defaultParameters(String name, {int age = 10}) {
  print("defaultParameters: name is $name and age is $age");
}

void optionalParameters(String name, [int age]) {
  print("optionalParameters: name is $name and age is $age");
}

void main() {
  defaultParameters("john", age: 20);
  defaultParameters("john");
  
  optionalParameters("john");
  optionalParameters("john", 20);
}
```

## Static constructors

```dart
class Circle {
  static const pi = 3.142;
  
  static void drawCircle() {
    print(pi);
  }
}

void main() {
  print(Circle.pi);  
  Circle.drawCircle();
}
```

## Error Handling and custom Exceptions

```dart
class InputException implements Exception {
  String customException () {
    return "The input of negative number is not valid";
  }
}

void main() {
  try {
    var res = 4 / 0;
    print("$res");
  } on IntegerDivisionByZeroException {
    print("You cannot divide by zero, the value is undefined");
  }
  
  try {
    var res = 4 ~/ 0;
    print("$res");
  } catch (e) {
    print("The exception is thrown: $e");
  }
  
  try {
    var res = 4 ~/ 0;
    print("$res");
  } catch (e, s) {
    print("The exception is: $e");
    print("The stack trace is: $s");
  }
  
  try {
    inputValue(0);
  } catch (e) {
    print("CustomError: $e, $e.customException()");
  }
  
}

void inputValue(int val) {
  if (val <= 0) {
    var inputException = InputException();
    throw inputException;
  }
}
```

## Anonymous functions

```dart
class Cart {
  Function addingTwoItems = (int a, int b) {
    var sum = a + b;
    return sum;
  };
  
  var shorthandSum = (int a, int b) => a + b;
}

void main() {
  var cart = Cart();
  print(cart.addingTwoItems(1, 2));
  print(cart.shorthandSum(10, 20));
}
```


## Implementing Callable

```dart
class CallableClassWithoutInput {
  String input = "Callable class";
  void call() {
    print(input);
  }
}

class CallableClassWithInput {
  void call(String input) {
    print(input);
  }
}

void main() {
  var call1 = CallableClassWithoutInput();
  call1();
  var call2 = CallableClassWithInput();
  call2("hello world");
}
```

## Future

```dart
Future<String> checkingStatus () {
  Future<String> result = Future.delayed(Duration(seconds: 1), () {
    return "OK";
  });
  
  return result;
}

void main() async {
  checkingStatus().then((result) {
    print(result);
  });
  
  var result = await checkingStatus();
  print(result);
}
```

## Stream

```dart
Stream<int> countStream(int to) async* {
  for (int i = 0; i < to; i++) {
    yield i;
  }
}

Future<int> sumStream(Stream<int> stream) async {
  var sum = 0;
  await for (var i in stream) {
    sum += i;
  }
  return sum;
}

void main() async {
  var stream = countStream(10);
  var sum = await sumStream(stream);
  print(sum);
}
```
