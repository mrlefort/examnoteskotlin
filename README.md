# examnoteskotlin

https://github.com/eguahlak/2016b-sem4-template-master-detail -- Eksempler + pensum osv.
## Operator Overloading Example


```kotlin
	data class Rational(val numerator: Int, val denominator: Int)

	
	operator fun Rational.times(other: Rational) =
	    Rational(this.numerator*other.numerator, this.denominator*other.denominator)

	
	
	operator fun Int.times(other: Rational) =
	        Rational(this*other.numerator, other.denominator)

	
	fun main(args: Array<String>) {
	    val x = Rational(2, 5)
	    val pi = Rational(22, 7)
	    println("$x * $pi = ${x*pi}")
	    val r = 34*pi*x
	    val q = 34.times(pi).times(x)
	    println("34*pi = ${34*pi}")
	    }
```

Dette er syntaxen for at overskrive en operator, dette er brugbart hvis du fx, skal gange mange brøker fordi der ikke er nogen standard implentation af gange i forhold til brøker.



## Extension Functions
```kotlin
fun Fragment.toast(message: CharSequence, duration: Int = Toast.LENGTH_SHORT) { 
  Toast.makeText(getActivity(), message, duration).show()
}
```

Dette kunne også gøres på en activity eller en context - i dette tilfælde har vi lavet en extension function på Fragment klassen. Dette gør det muligt fremover at kalde:
```kotlin
fragment.toast("Hello world!")
```

Hvis man i stedet tilføjede det på Context klassen kan vi droppe helt at bruge objektet som argument og bare skrive functionen:
```kotlin
fun Context.toast(message: CharSequence, duration: Int = Toast.LENGTH_SHORT) {
    Toast.makeText(this, message, duration).show()
}
```
Her har vi endda givet toast() functionen en default value på property'en 'duration', og vi kan derfor kalde metoden således: (uden objekt)
```kotlin
toast("Hello world!")
toast("Hello world!", Toast.LENGTH_LONG)
```


## Delegated Properties
```kotlin
class Example {
var p: String by Delegate()
}
class Delegate {
operator fun getValue(thisRef: Any?, property: KProperty<*>): String                              {
return "$thisRef, thank you for delegating '${property.name}' to me!" }
operator fun setValue(thisRef: Any?, property: KProperty<*>, value: String) {
println("$value has been assigned to '${property.name} in $thisRef.'") }
}
```
Delegate er en måde at lave custom getters og setters på som kan kaldes ved at sætte by delegate() på evt strings som så alle kalder den samme getter og setter metode.

Eksempel fra anders repo
https://github.com/eguahlak/2016b-sem4-template-master-detail/blob/master/app/src/main/java/dk/kalhauge/Adapter.kt

Companion Object
The companion object basically provides a place where one can put 'static' methods. Further more, a companion object, or companion module, has full access to the class members, including private ones. Companion Objects are great for encapsulating things like factory methods. Instead of having to have Foo and FooFactory everywhere, you can have a class with a companion object take on the factory responsibilities.


## Collections

MutableList is a subtype of List<T>

Immutable collection is basically read only meaning you cannot change, add or delete values in the collection.

Where as MutableList allows you to change, add or delete values.

### Example of useage

```kotlin
val numbers: MutableList<Int> = mutableListOf(1, 2, 3)
val readOnlyView: List<Int> = numbers
println(numbers)        // prints "[1, 2, 3]"
readonlyviews.add(1) // Would give an error since you cannot add on a immutablelist
numbers.add(4)
println(readOnlyView)   // prints "[1, 2, 3, 4]"
readOnlyView.clear()    // -> does not compile
```

## Ranges


In ranges can you use .. as an equivalent of integer loop in java.

In ranges you can use step to determine how much incrementing should happen etc in java:
```java
for(int i = 0; i<10; i+=2)
{
}
```
Here we increment every time by two. so it should run 5 times. 
the equivalent in kotlin would be:

```kotlin
for (i in 1..4 step 2) print(i) // prints "13"
```

### Example of useage
```kotlin
if (i in 1..10) { // equivalent of 1 <= i && i <= 10
    println(i)
}


for (i in 1..4) print(i) // prints "1234"

for (i in 4..1) print(i) // prints nothing

for (i in 4 downTo 1) print(i) // prints "4321"

for (i in 1..4 step 2) print(i) // prints "13"

for (i in 4 downTo 1 step 2) print(i) // prints "42"

for (i in 1 until 10) { // i in [1, 10), 10 is excluded
     println(i)
}
```


## Lambdas

A lambda expression or an anonymous function is a "function literal", i.e. a function that is not declared, but passed immediately as an expression.

### Example of useage
```kotlin
val numbers: MutableList<Int> = mutableListOf(1, 2, 3)   
    
    numbers.map { it -> // sends it to next function.
                 var lol = it * 2; // lol = mutableListOf(1*2, 2*2, 3*2)
                 lol = lol * 10;  // lol =  mutableListOf(2*10, 4*10, 6*10)
                 println(lol) // prints 20, 40, 60
                } 
		
		    numbers.map { // does not need arrow function if only one operation is run.
                 println(it*5) // prints 5, 10, 15
                } 
		
```
