## Injecting inside the ViewModel using `by inject()`

```kotlin
class SabadosViewModel(courier: Courier?) : ViewModel(), KoinComponent {
    private val repository by inject<InfoSabadoRepository>()
}
```

#### What happens here:
- `courier` is passed manually when the ViewModel is created.
- `repository` is injected **inside** the ViewModel using Koin’s `by inject()` delegate.
- The ViewModel must implement `KoinComponent` to access Koin’s injection API.

#### - Harder to test (you need to start Koin in tests or mock the injection).

## Option 2: Injecting everything via constructor

```kotlin
class SabadosViewModel(
    private val repository: InfoSabadoRepository,
    private val courier: Courier?
) : ViewModel()
```

#### What happens here:
- Both `repository` and `courier` are passed directly into the constructor.
- Koin will inject `repository` automatically if it's declared in a module.
- `courier` can still be passed manually using `parametersOf()`.

#### Pros:
- **More testable**: You can easily create the ViewModel in unit tests without Koin.
- **More explicit**: All dependencies are visible in the constructor.
- **No need for `KoinComponent`**.

#### Cons:
- Slightly more boilerplate in the Koin module if you have many parameters.

### ✅ Recommendation

If you're aiming for **clean architecture and testability**, go with **constructor injection**:

```kotlin
class SabadosViewModel(
    private val repository: InfoSabadoRepository,
    private val courier: Courier?
) : ViewModel()
```

And in your Koin module:

```kotlin
viewModel { (courier: Courier) -> SabadosViewModel(get(), courier) }
```

Would you like help updating your Koin module and ViewModel to use this cleaner constructor-based approach?
