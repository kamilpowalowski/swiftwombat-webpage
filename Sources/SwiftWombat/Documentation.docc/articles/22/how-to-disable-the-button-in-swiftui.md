# How to disable the button in SwiftUI

@Metadata {
    @PageImage(purpose: card, source: how-to-disable-the-button-in-swiftui)
}

In your SwiftUI applications, you will be using Button view very often. Simple user inputs are built using this interactive control. But in this article, you will learn how to make buttons disabled.

##

Think about a situation as follow - you have three different options, but some of them are only active when the toggle is true. You can hide inactive options using the `if` statement, but this will be counterintuitive for users. The "Don't make me think" principle assumes that users should know what's going on and not be surprised by UI. You can achieve it by just disabling that options.

To `disable` a button, you should use the disabled view modifier. It takes a bool parameter, which for example, can be taken from the state.

```swift
@State private var disabled = true

var body: some View {
    Button("Press me", action: {})
        .disabled(disabled)
}
```

You can use the `disabled` modifier on the view above buttons (`VStack`, for example). That way, you will apply it to all buttons (or other controls below).

```swift
VStack {
    Button("Press me 1", action: {})
    Button("Press me 2", action: {})
    Button("Press me 3", action: {})
}
.disabled(true)
```

> According to [the documentation](https://developer.apple.com/documentation/swiftui/list/disabled(_:)), `disabled` from a view higher in scope takes precedence over disabled from lower views. But my experiments (you can find a link to the project below) show that priority has one that its parameter is set to `true` and order is not important.

![Disable button Xcode Example](disable-button-xcode-example)

Want to test it yourself? Download this [Xcode Project](https://github.com/kamilpowalowski/swiftwombat-webpage/).
