# Enum

---

## ✅ Use `enum` when:

### 🔒 1. You have a **fixed set of known options**

Like:

* UI modes: `LIGHT`, `DARK`, `SYSTEM_DEFAULT`
* Sort options: `ASCENDING`, `DESCENDING`
* App states: `LOADING`, `SUCCESS`, `ERROR`

```kotlin
enum class ThemeMode {
    LIGHT, DARK, SYSTEM_DEFAULT
}
```

---

### 🔤 2. You want to **avoid magic strings or numbers**

Instead of:

```kotlin
val sort = "asc" // typo risk!
```

Do:

```kotlin
val sort = SortOrder.ASCENDING
```

✅ Type-safe
✅ Compiler catches mistakes
✅ Easier to refactor

---

### 🧪 3. You need **clean branching logic**

```kotlin
when (sortOrder) {
    SortOrder.ASCENDING -> ...
    SortOrder.DESCENDING -> ...
}
```

The compiler ensures you **handle every case**.

---

### 🛠️ 4. You want to **associate small bits of static data**

```kotlin
enum class HttpStatus(val code: Int) {
    OK(200),
    NOT_FOUND(404),
    SERVER_ERROR(500)
}
```

---

## ❌ Don’t use `enum` when:

| Situation                                       | Use instead                         |
| ----------------------------------------------- | ----------------------------------- |
| You need different fields per case              | 🔁 `sealed class`                   |
| You want to return different behavior per state | 🔁 `sealed class`                   |
| You have dynamic or user-defined values         | 🔁 `String`, `Int`, or model class  |
| You need logic per type (e.g. `calculate()`)    | 🔁 `sealed class` with polymorphism |

---

