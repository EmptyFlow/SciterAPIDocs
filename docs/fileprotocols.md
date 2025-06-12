## Register file protocols

### How to register new custom protocol

```csharp
host.Callbacks.AddProtocolHandler (
  "embedded://", // custom protocol will be handled as embedded://my/resource/address/path
  (
  path => {
    return Encoding.UTF8.GetBytes ( // just always return same content for all addresses
      """"
      <!DOCTYPE html>
      <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
      <html>
      <body>
          <span id="world">Hello world!!!</span>
      </body>
     </html>
     """"
    );
  }
));
```

### Register existing protocol with partually handling

```csharp
host.Callbacks.AddProtocolHandler (
  "https://", // default protocol but we need to handle only few addresses
  (
  path => {
    if (path != "index.html/mycustomresource") return new byte[0]; // we handle only one address, others will be handled as usual

    return Encoding.UTF8.GetBytes ( // just always return same content for all addresses
      """"
{
"res": 100
}
      """"
    );
  }
));
```
