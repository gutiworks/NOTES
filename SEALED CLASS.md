# SEALED CLASS

---
### Basically one abstract class with multiple subclasses - each it's own object with different fields and behaivors
---

When you create a `sealed class`, **Kotlin forces all its subclasses to be declared in the same `.kt` file** — even if they’re in separate classes inside that file.

```kotlin
// UiState.kt
sealed class UiState {
    object Loading : UiState()
    data class Success(val data: String) : UiState()
    data class Error(val message: String) : UiState()
}
```

✅ You control exactly what kinds of `UiState` exist
❌ Nobody can create new types like `class Confused : UiState()` somewhere else in the codebase

---

## ✅ Why is this good? → Compiler **knows all the types**

Because Kotlin sees all the subclasses *right there in the file*, it knows the full list of possibilities. That’s important for the next point...

---

## ✅ Exhaustive `when` — no `else` needed

Let’s say you're doing this:

```kotlin
fun renderState(state: UiState) {
    when (state) {
        is UiState.Loading -> println("Loading...")
        is UiState.Success -> println("Data: ${state.data}")
        is UiState.Error -> println("Error: ${state.message}")
    }
}
```

### 👉 The compiler is happy.

✅ You don’t need an `else` block — because Kotlin knows you've covered **all possible cases**.

---

## ❌ What if you used an abstract class?

```kotlin
abstract class UiState

class Loading : UiState()
class Success(val data: String) : UiState()
class Error(val message: String) : UiState()
```

Now try:

```kotlin
fun renderState(state: UiState) {
    when (state) {
        is Loading -> println("Loading")
        is Success -> println("Success")
        is Error -> println("Error")
        // ❗ Compiler forces you to write `else ->` here!
    }
}
```

⚠️ Why? Because with `abstract class`, **someone might add a new subclass later**, and the compiler can’t know the full set. So Kotlin **makes you handle the `else`** just in case.

---

## ✅ Summary

| Concept                        | Sealed class              | Abstract class         |
| ------------------------------ | ------------------------- | ---------------------- |
| Subclasses in same file?       | ✅ Yes (compiler-enforced) | ❌ No (can be anywhere) |
| Compiler knows all subclasses? | ✅ Yes                     | ❌ No                   |
| Can skip `else` in `when`?     | ✅ Yes — exhaustive        | ❌ No — `else` required |

---

## 💡 Mental Model

> `sealed class` = a **closed list of allowed types**
> `abstract class` = an **open type**, can be extended anywhere

So if you're building something like:

* A UI that’s either **Loading**, **Success**, or **Error**
* An API response that’s **Ok**, **BadRequest**, or **Unauthorized**

You want `sealed class` because Kotlin can help ensure your code handles **every case**, with no surprises.
