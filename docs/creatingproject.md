## Prerequisites

* You need to download [https://gitlab.com/sciter-engine/sciter-js-sdk/-/releases](Sciter SDK).
* You need install [https://dotnet.microsoft.com/en-us/download](dotnet).

## Prepare C# project

Create C# project  
```shell
dotnet new create console --language=C# --name=TestProjectName
```
Add Sciter Package  
```shell
dotnet add test.csproj package EmptyFlow.SciterAPI
```

## Write basic startup code

```csharp
using EmptyFlow.SciterAPI;

namespace MyProjectNamespace {

	public static class Program {

		[STAThread] // fix many small issues for Windows OS
		public static void Main () {
                  var host = new SciterAPIHost (Environment.CurrentDirectory); // you need specify folder where will be located sciter library file (sciter.dll/libsciter.so/libsciter.dylib)
                  host.CreateWindow (asMain: true); // create main window
                  host.LoadFile ( "file://path/my.html" ); // load HTML page, path specified in first argument
                  host.Process (); // start sciter and run main loop for show main window
                }
        }
}
```

