## Event Handlers

It has two types of handlers - window and element (or html tag).  
The difference between these types is that EventHandler with window type can receive all events from all elements on the page while EventHandler with element type only events from that element. 
Basic class for all EventHandler's is `SciterEventHandler`. 
Also for convinience there is have two classes for each type - `WindowEventHandler` and `ElementEventHandler`.

## What is EventHandler?

EventHandler is class `SciterEventHandler` or one from it ancestors.
Inside class you can define handler by override some of virtual methods.  
You can check below which methods can be overridden:

### AfterRegisterEvent

Occurs immediately after EventHandler was registered.

### HandleInitializationEvent

Occurs when EventHandler was attached/deattached to element/window.

### ScriptMethodCall

Occurs when a JavaScript xcall(...) call on a element or window.

### BehaviourEvent

### SOMEvent

### MethodCall

Occurs when some of standart element methods called.

### ExchangeParameters

### DataArrived

### DrawEvent

In this event handler you can write custom logic for drawing.

### GestureEvent

Occurs when some of gesture happened.

### SizeEvent

Occurs after size of element changed.

### TimerEvent

### ScrollEvent

Occurs after scrolling.

### FocusEvent

### KeyboardEvent

### MouseEvent

### MouseEvent

## Attach EventHandler for window

```csharp
// create main window
host.CreateMainWindow ( ... ); 

// after window is created we can attach EventHandler for main window
host.AddWindowEventHandler ( new MyWindowEventHandler ( host.MainWindow, host ) ); 

// we inherit class from WindowEventHandler and override BehaviourEvent
// and inside it we can as example handled event happened after document is fully loaded
public class MyWindowEventHandler : WindowEventHandler {

    public MyWindowEventHandler ( nint window, SciterAPIHost host ) : base ( window, host ) {
    }

    public override void BehaviourEvent ( BehaviourEvents cmd, nint heTarget, nint he, nint reason, SciterValue data, string name ) {
        if ( cmd == BehaviourEvents.DOCUMENT_READY ) {
           // there can be your logic
        }
    }

}

```

## Add EventHandler for element from CSS property

First you need to add a factory to create you custom `SciterEventHandler`:

```csharp
host.Callbacks.AddAttachBehaviourFactory ( "mybehaviour", ( element ) => new MyCustomEventHandler ( element, host ) );
```

After it you can attach registered custom SciterEventHandler in CSS class or tag style:
```css
// in CSS

.customClass {
   behavior: 'mybehaviour'
}

<div class="customClass">
</div>
```

```html
<div style="behavior: 'mybehaviour'">
</div>
```

## Add EventHandler for element via SciterAPI

```csharp
// create event handler
var eventHandler = new SciterEventHandler();

// attach eventHandler with element
host.AddEventHandler(eventHandler);
```
