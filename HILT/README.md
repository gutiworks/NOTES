# HILT

Project gradle

```bash
plugins {
    id("com.google.dagger.hilt.android") version "2.56.2" apply false
}
```

App gradle

```bash
plugins {
    id("org.jetbrains.kotlin.kapt")
    id("com.google.dagger.hilt.android")
}
dependencies {
    //Hilt
    implementation("com.google.dagger:hilt-android:2.56.2")
    kapt("com.google.dagger:hilt-android-compiler:2.56.2")
}
```
