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
