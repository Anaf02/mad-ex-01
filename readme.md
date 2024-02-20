# MAD - Exercise 01

## Tasks

- Watch the Kotlin Crashcourse Video in Moodle or complete the tutorials **[Introduction to programming in Kotlin](https://developer.android.com/courses/pathways/android-basics-compose-unit-1-pathway-1)** and **[Kotlin fundamentals](https://developer.android.com/courses/pathways/android-basics-compose-unit-2-pathway-1)**.
- Answer the questions inside this Readme.md file and push it to your repository.
- Submit your coding solution of the Number Guessing Game inside the repository.
- Submit the link to your repository in Moodle.

## Questions

### Describe how Kotlin handles null safety. What are nullable types and non-null types in Kotlin? (0,5 points)

<span style="color:blue">Answer: </span>

Nullable types are variables which can hold "null" and non-null types are variables which cannot hold "null".
For a type to be nullable we have to add the ? operator at the end of the type because by default, the compiler infers that it is a non-null type.

```kotlin
	var a: Int = 10 // non-null type
	var b: Int? = 5 // nullable type
//     a = null // not possible -> Null can not be a value of a non-null type Int
	b = null //is possible
```

Null safety is a guarantee that no accidental calls are made on potentially null variables, which means that if we want to use the properties of a nullable type, the variable must not be null.
<br>In this example:

```kotlin
var c: String? = "exercise"
println(c.length)
```

the code generates the error -
"Only safe (?.) or non-null asserted (!!.) calls are allowed on a nullable receiver of type String?" because there is a chance that the variable "c" might be null and so we cannot acces its length property.

Ways to handle null safety in Kotlin:
<br>a. using the ?. safe-call operator

```kotlin
var c: String? = "exercise"
println(c?.length) //output as expected: 8, because the call is  made safe
c = null
println(c?.length) //output as expected: null
```

<br>b. using the !! not-null assertion operator (used only when we are sure that the variable isn't null)

```kotlin
var c: String? = "exercise"
println(c!!.length) //output as expected: 8, because the call asserts that the value isn't null
c = null
println(c!!.length) //NullPointerException, because the value is actually null and we cannot consider it non-null
```

<br>c. if/else conditionals
<br>Simply check if the variable is null before using it:

```kotlin
if (c != null) {
      println("The length of the variable is ${c.length}.")
    } else {
      println("The variable is null, input a value.")
    }
```

Assigning an if/else expression to a non-nullable type:

```kotlin
val variableLength = if (c != null) {
 c.length
} else {
 0
}
```

<br>d. using the ?: Elvis operator (used as an addition to the ?. safe-call operator)

```kotlin
   var c: String? = null
   val variableLength = c?.length ?: 0 // if the variable is not null the expression on the left of the Elvis operator will be executed,
                                       //otherwise the right expression - in this case, since c is null, the length will be assigned the value 0
```

### What are lambda expressions and higher order functions in Kotlin? Why would you store a function inside a variable? (0,5 points)

<span style="color:blue">Answer</span>

Lambda expressions are a concise way of defining functions - the syntax for defining lambdas is without the fun keyword. Lambda expressions can be stored inside a variable without using the reference operator "::".
<br>Higher-order functions are functions that take other functions as parameters or return a function.
<br>Lambda expressions are useful when we need to pass a function as an argument or return a function as result because they can be stored inside a variable. This is useful since it's a good practice to reuse a function multiple times.

### Provide a solution for the following number guessing game inside `App.kt`. (3 points)

## Number Guessing Game in Kotlin

The game is a simple number guessing game. The task is to generate a random, max 9-digit, number. The number must **not contain repeating digits**. Valid digits are 1-9.
Ask the user to guess the max 9-digit number. The game is finished when the user guesses the correct digits in the correct order.
In each round, the user gets feedback about the number of correct digits and the number of correct digits in the correct position.
The output should be in the format "n:m", where "n" is the number of digits guessed correctly regardless of their position,
and "m" is the number of digits guessed correctly at their correct position. Here are some examples:

This example shows the game flow with 4-digits to guess (the default argument)

Generated number: 8576

- User input: 1234, Output: 0:0
- User input: 5678, Output: 4:1
- User input: 5555, Output: 1:1
- User input: 3586, Output: 3:2
- User input: 8576, Output: 4:4 -> user wins

Take a look into the provided code structure in `src/main/kotlin/App.kt`. Implement the following methods (lambda expressions):

- _playNumberGame(digitsToGuess: Int = 4)_ (1 point): The main game loop that handles user input and game state. Make use of _generateRandomNonRepeatingNumber_ and _checkUserInputAgainstGeneratedNumber_ here. This function also utilizes a default argument
- _generateRandomNonRepeatingNumber_ (1 point): A lambda expression that generates a random number with non-repeating digits of a specified length.
- _checkUserInputAgainstGeneratedNumber_ (1 point): A lambda expression that compares the user's input against the generated number and provides feedback.

`CompareResult.kt` This class is a data structure which helps with bundling the result of the comparison of the user input and the generated number. Look at the toSting() and use it in your output.

Run the project with `./gradlew run` and test your implementation with the provided tests in `src/test/kotlin/AppTest.kt` with `./gradlew test`.

# Project Structure

The project is structured into two main Kotlin files:

**App.kt**: Contains the main game logic and functions.

**AppTest.kt**: Contains unit tests for the various functions in App.kt.
