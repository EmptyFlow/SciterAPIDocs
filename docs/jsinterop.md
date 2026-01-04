## JavaScript Interop

Usually, to interact with JavaScript, we need to either execute some code from C# on the JavaScript side or get value(s) from the JavaScript side in C#.

### How to execute JavaScript code from C#?

First of all, any JavaScript code performed inside window scope, which mean we need to know window.  
After it we can write code as follow:
```csharp
// our window pointer
var windowPointer = ...;
// script that will be performed in window scope
var script = '2 + 3';

SciterValue result;

// evaluate
Host.ExecuteWindowEval(windowPointer, script, out result);

var calculatedValue = Host.GetValueInt32(ref result);

Console.WriteLine("Result is " + calculatedValue);
```

### How to execute C# code from JavaScript?

With EventHandler we can handle a lot of changes to an element, but what if we want to literally call C# methods from JavaScript?
We can do this, but it will look like we are handling an event from the element.  

First of all we need to markup as follow:
```html
...
<!-- we define some element in HTML and attach our behaviour -->
<div id="myid" style="behavior: mybehaviour"></div>
...
<script>
const element = document.getElementById('myid');
const result = element.xcall("csharpmethod", "string1", 1);
console.log(result);
</script>
```

Second we need to handle call in C# and to do something:
```csharp
public class MyHandler : ElementEventHandler {

    public MyHandler ( nint element, SciterAPIHost host ) : base ( element, host ) {}

    public override (SciterValue? value, bool handled) ScriptMethodCall ( string name, IEnumerable<SciterValue> arguments ) {
	// only if called csharpmethod
        if ( name == "csharpmethod" ) {
                // read first string parameter
		var stringParameter = arguments.ElementAt ( 0 );
		var stringValue = Host.GetValueString(ref stringParameter);
                // read second number parameter
		var intParameter = arguments.ElementAt ( 1 );
		var intValue = Host.GetValueInt32(ref intParameter);
                // create result value
		return (Host.CreateValue(stringValue + intValue), true);
	}

        return (null, false);
    }
```
