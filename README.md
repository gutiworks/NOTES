# NOTES

[Functional Interface](#@functionalinterface)

[Default methods](#default-methods)

[Static methods](#static-methods)

---

### @FunctionalInterface

Para indicar que una interfaz solo contiene un método abstracto

```bash
@FunctionalInterface
public interface MyFunction {
    int apply(int a, int b);
}

MyFunction add = (a, b) -> a + b;
System.out.println(add.apply(5, 3)); // Salida: 8

```

---

### Default methods

Provide a concrete implementation inside an interface

```bash
public interface MyInterface {
    void doSomething(); // abstract method

    default void log(String message) {
        System.out.println("LOG: " + message);
    }
}
```

---

### Static methods

Thez belong to the class itself not from the instance

```bash
public interface MyInterface {
    void doSomething(); // abstract method

    default void log(String message) {
        System.out.println("LOG: " + message);
    }
}

Utilidades.imprimirMensaje("Hola, mundo!"); // Salida: Hola, mundo!
```

---

