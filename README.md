# **Deprecated**
## This was an early attempt to get SVG to load with Glide, while it does work it does not support image tinting and probably some other things that I have not noticed yet.
## I have since found a better library that does support tinting etc: [Glide SVG](https://github.com/qoqa/glide-svg). ([![](https://jitpack.io/v/qoqa/glide-svg.svg)](https://jitpack.io/#qoqa/glide-svg))
## I will no longer be maintaining this library.
---

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
