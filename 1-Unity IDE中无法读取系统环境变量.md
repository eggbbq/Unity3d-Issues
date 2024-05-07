# Unity IDE中无法读取系统环境变量
在terminal中访问环境变量正常，但是unity中无法访问环境变量
```c#
//示意
var psi = new ProcessStartInfo()
{
    CreateNoWindow = false,
    FileName = "dotnet",
    StandardErrorEncoding = Encoding.UTF8,
    StandardInputEncoding = Encoding.UTF8,
    StandardOutputEncoding = Encoding.UTF8,
    RedirectStandardError = true,
    RedirectStandardOutput = true,
    UseShellExecute = false,
};

var p = Process.Start(psi);
var log = p.StandardOutput.ReadToEnd();
Debug.Log(log);

/**
Win32Exception: ApplicationName='dotnet', CommandLine='', CurrentDirectory='', Native error= Cannot find the specified file
System.Diagnostics.Process.StartWithCreateProcess (System.Diagnostics.ProcessStartInfo startInfo)....
*/
```

Unity IDE 不会自己读取系统环境变量，而是从 Unity Hub继承。在Windows系统环境下，Unity Hub启动时会读取系统的环境变量，但是在Macos系统下，点击Unity Hub由于某些原因是无法读取到某些环境变量的。

解决方案如下

1) Macos直接在Termial中启动 Unity Hub，这样Unity Hub就能继承Terminal的变量。“/Applications/Unity Hub.app/Contents/MacOS/Unity Hub”

2) Windows系统遇到无法访问环境变量大概率是，在Unity Hub运行过程中，新添加的环境变量无法访问。退出Unity IDE 和 Hub，重新启动即可