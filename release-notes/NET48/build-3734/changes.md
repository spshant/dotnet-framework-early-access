# .NET Framework Build 3734 Release Notes
Following changes are included in .NET Framework 4.8 build 3734. You can view the full list of [.NET Framework 4.8 Changes](/release-notes/NET48/dotnet-48-changes.md) (all changes, including those in build 3734 and builds upto current date).

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## ASP.NET

* Fixed handling of multi-value HTTP headers that may affect multipart data processing. [726155, System.Web.dll, Bug, Build:3734]
* For client applications (winforms, WPF, or console apps, etc) the ASP.NET Client Application Services API’s have been hardened against potentially malicious JSON payloads. [727703, System.Web.dll, Bug, Build:3734]
* Fixed an issue introduced in ASP.NET 4.7, where the unexpected removal of a particular type of cache item can result in an orphaned *.delete file that prevents web applications from running. [750653, System.Web.dll, Bug, Build:3734]

## BCL

* Fixed a serialization exception that occurred when a huge amount of objects were serialized with BinaryFormatter. [761576, mscorlib.dll, Bug, Build:3734]

## CLR

* Prevents applications from COM activating managed types whose GUIDs mismatch the declared CLSID in the registry" [752205, clr.dll, Bug, Build:3734]
* Fixed deadlocks that could occur when loading exception stack traces in out-of-memory conditions. [748860, diasymreader.dll, Bug, Build:3734]
* Improved scalability of System.Threading.Timer. Previously System.Threading.Timer had a single global queue that was protected by a single process-wide lock. This can become a scalability problem if Timers are used frequently on multi-CPU machine. This change splits into N per-processor Queues as well as other improvements that improve the performance in a high-scale environment. For compatibility reasons this new code is not activated by default at the present time. It needs to be activated by using .NET Config variable ScalableTimer. [735923, clr.dll, mscorlib.dll, Bug, Build:3734]
```xml
<configuration>
  ...
  <runtime>
    <AppContextSwitchOverrides value=""Switch.System.Threading.UseNetCoreTimer=true""/>
  </runtime>
</configuration>
```
* Added an opt-in config option to disable spin-waiting for a critical section when contended. The change can be opted into in an <app>.exe.config file as follows: [754173, clr.dll, Bug, Build:3734]
```xml
<configuration>
  ...
  <runtime>
   <Crst_DisableSpinWait enabled=""1""/>
  </runtime>
</configuration>
```
* Fixed the output from the "!u -gcinfo" command in the SOS Debugging Extension [740360, sos.dll, Bug, Build:3734]
* Customers who are profiling their .NET Framework application will no longer experience leaks on their ICorProfilerCallback9 COM object as ICorProfilerCallback9 COM object is never freed in the destructor of EEToProfInterfaceImpl instance. [742282, clr.dll, Bug, Build:3734]
* Updated ICorProfilerInfo4::GetILToNativeMapping2 to respect the rejitID field and return the appropriate mapping. [748879, clr.dll, Bug, Build:3734]
* Fixed storing of instances to the mark stack so that the subsequent code that follows can operate by popping the stack. [750816, clr.dll, clrgc.dll, Bug, Build:3734]
* Fixed an issue in the JIT with the compilation of methods that use explicit tailcalls. This feature is never used by C# programs but can impact some F# programs. If you are developing an F# application, you may see incorrect results or program crashes. A workaround is to disable tailcalls or use a debug build of your F# program.   [754566, clrjit.dll, Bug, Build:3734]

## Networking

* Fixed handling of 1xx interim responses. [711440, System.dll, Bug, Build:3734]

## Windows Forms

* Added Scroll UIA pattern to ListBox items in order to make the control accessible. [742319, System.Windows.Forms.dll, Bug, Build:3734]
* Fixed ColorEditor, ContentAlignmentEditor, CursporEditor to respond to DPI changed messages and made changes in FontEditor to always open in the 'SystemAware' mode even when the application is in "per-monitor" mode. [746634, System.Windows.Forms.dll, System.Drawing.Design.dll, Bug, Build:3734]
* Fixed providing correct accessibility information and correct accessible hierarchy of PropertyGrid control. [526702, system.windows.forms.dll, Bug, Build:3734]
* The screen reader announcement of the WinForms' Menu and ToolStrip expandable subitems has been fixed to not read in items' and scan mode the hidden (collapsed) subitems until corresponding parent Menu item/ToolStrip DropDown item is expanded. In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. [560840, System.Windows.Forms.dll, Bug, Build:3734]
* Fixed UI Automation provided accessibility of WinForms DataGridView ComboBox to have appropriate and consistent screen reader announcement for ComboBox interactions. The feature is available starting with Windows 10, version 1709 (RS3). In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. [732559, System.Windows.Forms.Dll, Bug, Build:3734]  
In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file.
```xml
<configuration>
  ...
  <runtime>
    <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
    <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
    <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
  </runtime>
</configuration>
```

## WPF

* Improved the memory allocation and cleanup scheduling behavior of the weak-event pattern. To opt-in to these improvements, set AppContext switches to 'true': Switch.MS.Internal.EnableWeakEventMemoryImprovements and Switch.MS.Internal.EnableCleanupSchedulingImprovements. [759824, WindowsBase.dll, PresentationFramework.dll, Bug, Build:3734]
* Fixed context menus and popups that are sometimes dismissed unexpectedly when shown for the first-time on a non-primary High-DPI monitor [732853, PresentationFramework.dll, PresentationCore.dll, Bug, Build:3734]
* Fixed a crash due to ElementNotAvailableException arising when scrolling and expanding/collapsing nodes in a TreeView with VirtualizationMode=Recycling, that changes its IsEnabled property while expanding nodes. This crash only occurs when there is a "partial automation client" running (and no full automation client); The chief example is running the app over RDP to a Win10 machine. [705448, PresentationCore.dll, Bug, Build:3734]
* Fixed a crash in WPF when displaying specific Unicode characters (Unicode codepoint 0xFDFD 47 times or more in a row) [725381, PresentationCore.dll, Bug, Build:3734]
* Fixed the construction of automation for an ItemsControl to avoid calling the control's IsItemItsOwnContainerOverride method. This avoids crashes in cases where the override has bugs [755174, PresentationCore.dll, PresentationFramework.dll, Bug, Build:3734]
* Fixed an issue arising when removing an item from a grouped collection view. Any groups that become empty are themselves removed, raising CollectionChanged events before the parent groups' counts have been fully updated. An event handler that calls back into the collection view can get ArgumentOutOfRangeException. [765355, PresentationFramework.dll, Bug, Build:3734]
* In .NET 4.8 Preview, WPF programs that create many RenderTargets (e.g. RenderTargetBitmap) can leak GDI handles and memory eventually resulting in an OutOfMemoryException from System.Windows.Media.Composition.DUCE+Channel.SyncFlush(). This was due to a COM reference cycle keeping render targets alive in the WPF renderer. Fixed this issue. [756618, wpfgfx_v0400.dll, Bug, Build:3734]
