# HILT

Project gradle

```bash
plugins {
    id("com.google.dagger.hilt.android") version "2.56.2" apply false
    id("com.google.devtools.ksp") version "2.1.0-1.0.29" apply false
}
```

App gradle

```bash
plugins {
    id("com.google.devtools.ksp")
    id("com.google.dagger.hilt.android")
}
dependencies {
    //Hilt
    implementation("com.google.dagger:hilt-android:2.56.2")
    ksp("com.google.dagger:hilt-android-compiler:2.56.2")
}
```
