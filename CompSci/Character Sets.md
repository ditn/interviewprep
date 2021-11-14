# ASCII
128 characters, one byte per character.

# Extended ASCII
256 characters, one byte per character.

# Unicode
`a = 97` 
`b = 98`
`c = 99`
`...`
`z = 122`

Two bytes per character.

# Convert Char to number

```kotlin
"1234"[3] - '0' == 4
```

# Char to Index

```kotlin
"apple"[0] - 'a' == 0
```

# Number Range

```kotlin
'0'.toInt() == 48
'9'.toInt() = 57
```

e.g.:

```kotlin
fun parseInt(string: String): Int {  
    var num = 0  
  
 	string.forEach {  
 		if (it.toInt() in 48..57) {  
            num = num * 10 + (it - 48).toInt()  
        } else {  
            throw NumberFormatException("Invalid character $it")  
        }  
    }  
  
 	return num  
}
```