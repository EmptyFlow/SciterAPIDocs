## PseudoSOM

Sciter has a SOM function, but it's not supported in the SciterAPI. PseudoSOM can be used as an alternative.
The purpose of PseudoSOM (or PSOM) is to achieve the same thing, but through an event handler. PSOM has an internal and external form. The internal form is useful if you have a C# class as the source of the true value. The external form is useful if you want to create SciterValue values on the C# side.

## Inner

First of all you need to create model class. As example I create simple one:
```csharp
public class MyModel {

	public int Count { get; set; } = 5;
	
	public string Name { get; set; } = "Test";
	
}
```
After it we need to create event handler. You can do it manually:
```csharp
var host = // instance of SciterAPIHost
var windowPointer =  // window pointer
var element = // HTML element pointer
var modelName = "customModel" // name of property which will be accessible from JavaScript

var handler = new InnerPseudoSomModelHandler<MyModel>(new MyModel(), element, windowPointer, host, modelName);
```

Inside JavaScript you can do now there:

```javascript
var element = document.getElementById('myelement'); // you need to find element
// read value
console.log(element.customModel.count); // 5

// edit value
element.customModel.count = 50;
console.log(element.customModel.count); // 50
```

## Outer

Will be updated after implementation