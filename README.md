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


Delegated Properties
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
