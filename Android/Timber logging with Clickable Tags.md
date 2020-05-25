# Timber logging with Clickable Tags

In this tutorial we will look at how to use **Timber library** to log statements with Tags which are clickable.

-------

For this, first you need to add following dependency to your `build.gradle` file.

```
implementation 'com.jakewharton.timber:timber:4.7.1'
```

-------

After that, create a class `ClickableLoggingTree` and paste following code.

```kotlin
import timber.log.Timber

class ClickableLoggingTree: Timber.DebugTree() {

    override fun createStackElementTag(element: StackTraceElement): String? {
        with(element) {
            return "($fileName:$lineNumber)$methodName()"
        }
    }

}
```

Here we are using File Name, Line Number and Method Name.

-------

After that, you need to plan this tree in the `Application` SubClass.

```kotlin
Timber.plant(ClickableLoggingTree())
```

You can also plant different trees for each build variants. For example, you can plant a tree for debug build and a separate tree for release build.