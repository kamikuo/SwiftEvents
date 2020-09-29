# SwiftEvents
define and trigger events for class.

## Usage

Add protocol 'EventsOwner' to class and define events.
```swift
class SomeClass : EventsOwner {
    var someEvent: Event { return Event(name: "someEvent", owner: self) }
    
    func doSomeEvent() {
        someEvent.trigger()
    }
}
```
```swift
let someObject = SomeClass()
someObject.someEvent.addAction { _ in
    print("SomeEvent did trigger!")
}

someObject.doSomeEvent()
//SomeEvent did trigger!
```

### Example

Create a closure button.

```swift
class ClourseButton : UIButton, EventsOwner {
    override init(frame: CGRect) {
        super.init(frame: frame)
        addTarget(self, action: #selector(didClick), for: .touchUpInside)
    }
    
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    var clickEvent: SwiftEvents.Event { return SwiftEvents.Event(name: "click", owner: self) }
    @objc private func didClick() {
        clickEvent.trigger()
    }
}
```

## Lisence
The MIT License (MIT)
