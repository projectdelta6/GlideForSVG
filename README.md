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

### And and add a GlideHelper(or whatever you'd like to call it) class like this:
```kotlin
import android.graphics.drawable.PictureDrawable
import android.net.Uri
import android.widget.ImageView
import androidx.annotation.IntDef
import androidx.appcompat.app.AppCompatActivity
import com.bumptech.glide.RequestBuilder
import com.bumptech.glide.load.resource.drawable.DrawableTransitionOptions
import com.duck.glideforsvgmodule.SvgSoftwareLayerSetter

class GlideHelper(activity: AppCompatActivity) {

   /**
    * [GlideApp] implementation for 'Standard' image handling.
    */
   private val plainGlideRqBuilder: GlideRequests by lazy {
       GlideApp.with(activity)
   }

   /**
    * [GlideApp] implementation for SVG image handling.
    *
    * @see [com.duck.glideforsvgmodule.SvgGlideModule]
    */
   private val svgGlideRqBuilder: RequestBuilder<PictureDrawable> by lazy {
       GlideApp.with(activity)
           .`as`(PictureDrawable::class.java)
           .transition(DrawableTransitionOptions.withCrossFade())
           .listener(SvgSoftwareLayerSetter())
   }

   /**
    * Checks the [uri] to determine if the recourse is an SVG or not and invokes the appropriate
    * [GlideApp] implementation to load the image into the [target].
    *
    * @param uri The Uri representing the image. Must be of a type handled by [com.bumptech.glide.load.model.UriLoader].
    * @param target The view to cancel previous loads for and load the new resource into.
    */
   fun loadUriInto(uri: Uri, target: ImageView) {
       if(isSGV(uri)) {
           // Using svgGlideRqBuilder to load
           svgGlideRqBuilder
               .load(uri)
               .into(target)
       } else {
           // Using plainGlideRqBuilder to load Uri
           plainGlideRqBuilder
               .load(uri)
               .into(target)
       }
   }
   
   /**
    * @return True if the recourse is an SVG.
    */
   private fun isSGV(): Boolean {
       TODO("Add your logic to determine if the recourse is an SVG or not")
   }
}
```

### And Use in your code like this:

```kotlin
lateinit var glideHelper: GlideHelper

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    //...
    // init your GlideHelper (or whatever you decided to name it)
    glideHelper = GlideHelper(this)
    //...
    // Load an image into an ImageView:
    glideHelper.loadUriInto(yourImageUri, yourImageView)
}
```