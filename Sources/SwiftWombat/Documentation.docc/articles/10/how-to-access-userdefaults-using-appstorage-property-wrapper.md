# How to access UserDefaults using AppStorage property wrapper

@Metadata {
    @PageImage(purpose: card, source: how-to-access-userdefaults-using-appstorage-property-wrapper)
}

WWDC20 SwiftUI updates straight forwards `UserDefaults` access by introducing `@AppStorage` property wrapper. This article will explain how to store and read simple types like integer, string, double, data, or URL.

> Tip: Learn how to store other types like Date using RawRepresentable - <doc:how-to-store-a-date-using-appstorage-in-swiftui>

`UserDefaults` is a simple key-value storage that can be used to store a limited number of simple values. It is a simple persistence system where you can store user preferences or other, no critical, small data preserved between application runs.

To use `@AppStorage`, you have to wrap a property within your view with it. The only parameter that has to be specified is a string - the name of your key. Swift will deduce a type from a property itself.

```swift
@AppStorage("valueKey") var value: Int = 0
```

Your `@AppStorage` `UserDefaults` property is ready to use. You can read it and modify it in body function.

```swift
var body: some View {
    VStack {
        Text("Value: \(value)")
        Button("Increment") { value += 1 }
    }
}
```

When you change a property on one screen, any other that uses this property will also be refreshed. You can test it on that simple example.

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            ViewA()
            ViewB()
        }
    }
}

struct ViewA: View {
    @AppStorage("valueKey") var value: Int = 0
    
    var body: some View {
        VStack {
            Text("ViewA value: \(value)")
            Button("Increment") { value += 1 }
        }
    }
}

struct ViewB: View {
    @AppStorage("valueKey") var value: Int = 0
    
    var body: some View {
        VStack {
            Text("ViewB value: \(value)")
            Button("Decrement") { value -= 1 }
        }
    }
}
```

There is one additional detail worth mentioning — UserDefaults support different databases. By default, `@AppStorage` uses `UserDefaults.standard`, but you can create your own by providing it as a store parameter.

```swift
@AppStorage("valueKey", store: UserDefaults(suiteName: "com.swiftwombat.customStore")) var value: Int = 0
```

Values in different databases (created by providing a suite name) are not connected and can have the same key. Modifying value in the standard defaults doesn't alter the value in custom defaults.

![AppStorage example Xcode project](appstorage-example-xcode-project)

Want to test it yourself? Download this [repository](https://github.com/kamilpowalowski/swiftwombat-webpage/).


@Small { 2021-01-11 20:55 }
