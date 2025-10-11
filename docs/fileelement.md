## Working with HTML elements

### Using selectors throughout the page

If you want to select multiple elements on the entire page, you need to search by CSS selector.

```csharp
var foundElements1 = Host.MakeCssSelector ("#myid"); // found element with identifier - myid
var foundElements2 = Host.MakeCssSelector ("div"); // found all element with tag div on page
var foundElements3 = Host.MakeCssSelector (".myclass"); // found all element with class myclass
```

### Using selectors within an element

```csharp
var element = .... // an element within which you need to find some elements

var foundedElements = Host.MakeCssSelector(".someclass", element);
```

### Working with Text and HTML

```csharp
var element = ....

// for get Text from element
var elementText = Host.GetElementText(element);

// for set Text to element
Host.SetElementText(element, "New text inside element");

// for get HTML from element
var outer = false; // if outer true result value will be contains also tag of element itself
var elementHTML = Host.GetElementHtml(element, outer);

var insertMode = SetElementHtml.ReplaceContent; // mode reflect how and where new content will be inserted inside element
Host.SetElementHtml(element, "<span>New content inside element</span>", insertMode);

```

### Working with element styles

```csharp
var element = .... // an element

// This is how we can get value from style.
// We get value for style property background-color
var backgroundColor = Host.GetElementStyleProperty(element, "background-color");

// This is how we can set value to style.
// New color for style property background-color will be green.
Host.SetElementStyleProperty(element, "background-color", "green");

```

### Working with element attributes

```csharp
var element = .... // an element

// This is how we can get value from attribute with name style.
var attributeValue = Host.GetElementAttribute(element, "style");

// This is how we can get all attribute names in array.
var attributeNames = Host.GetElementAttributeNames(element);

// This is how we can check if element have some attribute or not .
var caseSensitiveMode = CaseInsensitiveMode.CaseInsensitive; // There is a parameter that affects how the name check will be performed.
var attributeNames = Host.GetElementHasAttribute(element, "somename", caseSensitiveMode);

// This is how we can get all attributes as dictionary from element.
var attributes = Host.GetElementAttributes(element);

// This is how we can set attribute to element.
Host.SetElementAttribute(element, "src", "http://myimages.com/myimage.jpg");

// we can delete all attributes from element
Host.ClearAttributes(element);

```
