# KOIN

## 1. With Parameters (Dynamic Injection)

```kotlin
val viewModelModule = module {
    viewModel { (courier: Courier) -> SabadosViewModel(courier) }
}
```

#### Use this when:
- Your `ViewModel` needs a parameter **at runtime** (e.g., passed from a Fragment).
- You don’t know the value of `courier` at the time of defining the module.

#### How you use it:
```kotlin
val courier = arguments?.getParcelable<Courier>("courier")!!
private val viewModel: SabadosViewModel by viewModel { parametersOf(courier) }
```

---

### 2. Without Parameters (Static Injection)

```kotlin
viewModel {
    SabadosViewModel(
        get() // Koin will inject this dependency automatically
    )
}
```

#### Use this when:
- Your `ViewModel` depends on something that is already defined in Koin (like a repository).
- You don’t need to pass anything manually at runtime.

#### Example:
```kotlin
class SabadosViewModel(private val repository: SabadosRepository) : ViewModel()
```

And in your module:
```kotlin
single { SabadosRepository() }
viewModel { SabadosViewModel(get()) }
```

