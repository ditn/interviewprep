# Hash Functions

Typically a hash function is _locality insensitive_, which means that a small change to the input results in a very large change to the output - you can't predict an output from a previous output and use it to work out if you're close to guessing a password.

```kotlin

"dog".md5() = "06d80eb0c50b49a509b49f2424e8c805"
"dot".md5() = "69eb76c88557a8211cbfc9beda5fc062"

```

However, this may be undesirable.

# Simhash
Simhash does the opposite. Small changes in a file or input result in small changes to a hash, allowing you to compute if two files are similar. This can be used to detect copyrighted materials, cheating/plagiarising, or detecting duplicates when crawling the web.