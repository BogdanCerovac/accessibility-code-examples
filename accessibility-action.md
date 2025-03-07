# Accessibility action

Accessibility actions provide alternative ways for for users of assistive technologies to perform actions. For users of [switch control](https://beta.appt.org/en/docs/ios/features/switch-control) it can be difficult to use drag-and-drop functionality. This functionality can be made more accessible by providing accessibility actions to move items up and down.

## Android

On Android, you can add actions for assistive technologies using the [`addAction`](https://developer.android.com/reference/kotlin/androidx/core/view/accessibility/AccessibilityNodeInfoCompat#addAction(androidx.core.view.accessibility.AccessibilityNodeInfoCompat.AccessibilityActionCompat)) method via [`AccessibilityNodeInfoCompat`](https://developer.android.com/reference/androidx/core/view/accessibility/AccessibilityNodeInfoCompat).

```kotlin
ViewCompat.setAccessibilityDelegate(view, new AccessibilityDelegateCompat() {
    @Override
    public void onInitializeAccessibilityNodeInfo(
        View host,
        AccessibilityNodeInfoCompat info)
    {
        super.onInitializeAccessibilityNodeInfo(host, info);
        AccessibilityActionCompat action = new AccessibilityActionCompat(
            AccessibilityNodeInfoCompat.ACTION_CLICK,
            "Appt action"
        );
        info.addAction(customClick);
    }
});
```

## iOS

On iOS, you can use [`UIAccessibilityCustomAction`](https://developer.apple.com/documentation/uikit/uiaccessibilitycustomaction) to add custom actions for assistive technologies. You can also use [`UIAccessibilityCustomRotor`](https://developer.apple.com/documentation/uikit/uiaccessibilitycustomrotor) to add custom actions to the [VoiceOver rotor](https://beta.appt.org/en/docs/ios/features/voiceover).

```swift
// Custom action
let customAction = UIAccessibilityCustomAction(
    name: "Appt action",
    actionHandler: { (action: UIAccessibilityCustomAction) -> Bool in
        // Logic
        return true
    }
)
accessibilityCustomActions = [customAction]

// Custom rotor
let customRotor = UIAccessibilityCustomRotor(name: "Appt rotor") { predicate in
    // Logic
}
accessibilityCustomRotors = [customRotor]
```

## Flutter

With Flutter, you can use [`CustomSemanticsAction`](https://api.flutter.dev/flutter/semantics/CustomSemanticsAction/CustomSemanticsAction.html) to add custom actions for assistive technologies. To implement specific functionality for assistive technologies it is also possible to add `onTap`, `onLongPress` or other callbacks to the `Semantics` widget. When you do this, it is important to make sure the child nodes do not implement a touch listener, or to use `excludeSemantics` to ignore these with the assistive technologies.

```dart
Semantics(
    customSemanticsActions: <CustomSemanticsAction, VoidCallback>{
        CustomSemanticsAction(label: 'Increment'): _incrementCounter,
    },
    onTap: () {
        _incrementCounter
    },
    excludeSemantics: true,
    child: TextButton(...)
);
```

## React Native

In React Native, you can add [`accessibility actions`](https://reactnative.dev/docs/accessibility#accessibility-actions) using the `accessibilityActions` and `onAccessibilityAction` properties.

```jsx
<View
  accessible
  accessibilityRole="adjustable"
  accessibilityActions={[{name: 'increment', label: 'Increment'}]}
  onAccessibilityAction={event => {
    if (event.nativeEvent.actionName === 'increment') {
      handleIncrement();
    }
  }}
/>
```

## Xamarin

Xamarin does not have built-in support for adding accessibility actions.

```csharp
Not available, contribute!
```
