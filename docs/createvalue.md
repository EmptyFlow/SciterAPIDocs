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
