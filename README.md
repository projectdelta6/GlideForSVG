# GlideForSVG

Android Library for adding a Glide SVG module to your Android project

[![](https://jitpack.io/v/projectdelta6/GlideForSVG.svg)](https://jitpack.io/#projectdelta6/GlideForSVG)

https://jitpack.io/#projectdelta6/GlideForSVG

## Add it to your module/build.gradle with:
```gradle
allprojects {
    repositories {
        ...
        maven { url "https://jitpack.io" }
    }
}
```
and:

```gradle
dependencies {
    // add Glide to your project
    implementation ("com.github.bumptech.glide:glide:4.11.0")
    kapt 'com.github.bumptech.glide:compiler:4.11.0'

    //GlideForSVG
    compile 'com.github.projectdelta6:GlideForSVG:{latest version}'
}
//apply kotlin annotation processor for kotlin
apply plugin 'kotlin-kapt'
```

## To be able to load SVG and other(png, jpeg, etc.) in your project:

### Add a 'normal' AppGlideModule in your project, eg:
```kotlin
import com.bumptech.glide.annotation.GlideModule
import com.bumptech.glide.module.AppGlideModule

@GlideModule
class YourGlideModuleNameHere: AppGlideModule() {
    // add your Glide customisation here...
}
```

### And Use in your code like this:
```kotlin
lateinit var glideRqBuilder: GlideRequests

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    //...
    // init your GlideRequests object
    glideRqBuilder = GlideApp.with(this)
    //...
    // Load an image into an ImageView(standard Glide process): 
    glideHelper
        .load(yourImageUri)
        .into(yourImageView)
}
```