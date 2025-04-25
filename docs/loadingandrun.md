## Load HTML page

You can load HTML page by default from local file `file://...` or from internet `http(s)://...`.
Also supported local (from application path) folder via `home://...` protocol.
For loading HTML page you need to call method `SciterApiHost.LoadFile(...)`.

```csharp
host.LoadFile ( "file://my/path/to/file/index.html" );
```

You can also implement your own file source via the Custom File protocol. For more information check out [page](fileprotocols.md). 

## Run Sciter loop

Main Sciter loop start handle events and show main window. Loop will be happened until if last opened window will be closed by user or programmatically.
Start loop look like this:

```csharp
var code = host.Process ();
if (code != 0) {
   // error handling logic
}
```

You can close the main window while the loop is running as follows:
```csharp
host.CloseMainWindow();
```
After this, all other open windows will also be closed.
  
To close any other non-main window, you can call another method:
```csharp
host.CloseWindow(windowHwnd); // windowHwnd is pointer on window
```






