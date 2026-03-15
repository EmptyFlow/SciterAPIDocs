## Create Value

You can create a standard value using `CreateValue` and several additional `CreateXValue` methods for special types.

How to create standart value:
```csharp
var value = host.CreateValue ( 456565 );
```
Standart values can follow types: bool, int, long, decimal, double, float, string, IEnumerable<ScriteValue>, IDictionary<string, SciterValue>  

How to create color value:
```csharp
var value = host.CreateColorValue ( 0 );
```

How to create duration value:
```csharp
var value = host.CreateDurationValue ( 30 );
```

How to create duration value:
```csharp
var value = host.CreateAngleValue ( 90 );
```

How to create secure string:
```csharp
var value = host.CreateSecureString ( "my little secret:)" );
```

How to create error string:
```csharp
var value = host.CreateError ( "error!" );
```

## Common operations

Clear value:
```csharp
host.ClearValue(value);
```

Isolate value:
```csharp
host.IsolateValue(value);
```

## Get primitive types

You can use one from methods for get original value:
```csharp
var intValue = host.GetValueInt32(value); // get int value
var longValue = host.GetValueInt64(value); // get long value
var doubleValue = host.GetValueDouble(value); // get double value
var stringValue = host.GetValueString(value); // get string value
```

## Array value
How to get count of elements in array:
```csharp
var countElementinArray = host.GetArrayOrMapCount(value);
```

How to get element in array by index:
```csharp
var valueByIndex2 = host.GetArrayItem(ref value, 2);
```

How to set element in array by index:
```csharp
var valueByIndex2 = host.SetArrayItem(ref value, 2, ref newValue);
```

How to append new element in array at end of array:
```csharp
var valueByIndex2 = host.AppendItemToArray(ref value, ref newValue);
```

## Object (map in sciter docs) value
How to get element in object by string key:
```csharp
var item = host.GetMapItem(ref map, "item");
```

How to set element in object by string key:
```csharp
host.SetMapItem(ref map, "item", ref newValue);
```

How to get object:
```csharp
var itemsAsDictionary = host.GetMapItems(ref map);
```

How to get element in object by index:
```csharp
var itemsAsDictionary = host.GetValueMapKey(ref map, index);
```

## How to execute value if it function?
```csharp
var parameters = new List<SciterValue> (); // need to fill if required pass parameters
var resultValue =  host.ValueInvoke(ref value, valueContext, parameters);
```
## How to make JavaScript eval in window context?
```csharp
var script = "5 + 30"
host.ExecuteWindowEval(window, script, out var result);
var computedValue = host.GetValueInt32(result); // computedValue = 35
```
## How to call function in window context?
```csharp
var functionName = "myfunction";
var parameters = new List<SciterValue>(); // if required fill parameters for function here
host.ExecuteWindowFunction(window, functionName, parameters, out var result);
// result of function will be in variable result
```

## Global predefined variables
Can be helpful in cases where you need to return some code and return simple type values (like true/false/null).
It can help to reduce count of allocations and calls of SciterAPI which can be improve performance in some cases.
```csharp
host.TrueValue - value of true
host.FalseValue - value of false
host.NullValue - value of null
```
