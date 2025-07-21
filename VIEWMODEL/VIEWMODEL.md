# VIEWMODEL

## What is ViewModelProvider?

ViewModelProvider is a class in Android's architecture components that is responsible for creating and managing ViewModel instances.

### Why do we need it?
Lifecycle awareness: It ensures your ViewModel survives configuration changes like screen rotations.
Scope management: It gives you the same ViewModel instance as long as you're in the same scope (e.g., the same Fragment or Activity).
Memory efficiency: It avoids recreating the ViewModel unnecessarily.

## What is a ViewModelProvider.Factory?
A Factory is a way to customize how a ViewModel is created.

### Why do we need it?
By default, ViewModelProvider can only create ViewModels with no-argument constructors. But what if your ViewModel needs some data to work—like a Courier object, a repository, or a user ID?

That’s where the Factory comes in. It lets you inject dependencies into your ViewModel when it's created.

```bash
// On the activity fragment instead of create a new instance of the VW we use the provider.
// Attaching it to the provider makes the VM lifecycle aware
        _viewModel = ViewModelProvider(this, SabadosViewModelFactory(dataSabados))[SabadosViewModel::class.java]

```

```bash
// On the same VM we use the Factory.
// Allows us to customize the current VM that it has no constructor by default

class SabadosViewModelFactory(private val dataSabados: Map<String, String>) : ViewModelProvider.Factory {

    override fun <T : ViewModel?> create(modelClass: Class<T>): T {
        if (modelClass.isAssignableFrom(SabadosViewModel::class.java)) {
            return SabadosViewModel(dataSabados) as T
        }
        throw IllegalArgumentException("Error SabadosViewModel")
    }
}
```
