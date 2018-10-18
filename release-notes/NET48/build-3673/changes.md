# .NET Framework Build 3673 Release Notes
Following changes are included in .NET Framework 4.8 build 3673. You can view the full list of [.NET Framework 4.8 Changes](/release-notes/NET48/dotnet-48-changes.md) (all changes, including those in build 3673 and builds upto current date).

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## ASP.NET

* Fixed NullReferenceException thrown from the page/control with only parameterized constructors with default values when targeting 4.7.2 [635479, System.Web.dll, Bug, Build:3673]
* Fixed a perf issue in HttpApplication instances pool in HttpApplicationFactory class. [639421, system.web.dll, Bug, Build:3673]

## BCL

* Fixed GetECDsaPublicKey to work with brainpool curves. [586452, System.Core.dll, Bug, Build:3673]
* Reduced the number of object finalizations that occur as a result of using X509Certificate2 and related types. [654137, mscorlib.dll, System.dll, System.Security.dll, Bug, Build:3673]
* Fixed formatting of Japanese date with year 1 (as first year of any era), the date will be formatted using 元 character and not year number “1”.  Example of the new formatted date behavior: 平成元年11月21日compared to old formatted date behavior 平成1年11月21日 [670097, mscorlib.dll, Bug, Build:3673]

## CLR
* CLR COM no longer returns E_INVALIDARG when marshalling a byref SafeArray from an Event Handler. [239541, WindowsBase.dll, Bug, Build:3673]
* Fixed a potential hang when a blocking GC is induced in low memory situations [374828, clr.dll, Bug, Build:3673]
* If you are using Server GC on a Skylake or later machine, you might notice that clr!SVR::t_join::join is taking a lot more CPU cycles. This is because clr!SVR::t_join::join uses the PAUSE instruction which takes a lot longer on Skylake+. This fix scales down the number of times it’s called when running on Skylake+ machine. [683269, clr.dll, Bug, Build:3673]

## Networking
* Fixed a deadlock scenario when ServicePoint.ConnectionLimit is updated and requests are sent at the same time. [528650, System.dll, Bug, Build:3673]

## Windows Forms
* Fixed accessible hierarchy of WinForms DataGridView control to represent its currently editing control (inner cell TextBox or ComboBox) as a child of corresponding editing cell. Added support of UIA notifications to DataGridView control. [442899, System.Windows.Forms.Dll, Feature, Build:3673]
* A ToolStrip item's tooltip is displayed now when a user uses a keyboard to focus the ToolStrip item.
This change is effective in applications that have Switch.System.Windows.Forms.UseLegacyToolTipDisplay value and either Switch.UseLegacyAccessibilityFeatures.3 value is set to false or application is built to target .NET version 4.8.
App.config file content example:
<?xml version=""1.0"" encoding=""utf-8""?>
<configuration>
  ...
  <runtime>
    <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
    <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
    <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false""/>
  </runtime>
</configuration>  [549360, System.Windows.Forms.dll, Bug, Build:3673]"
* Fixed DataGridView ComboBox accessible hierarchy. Introduced the support of ComboBox UIA notifications [642548, System.Windows.Forms.Dll, Bug, Build:3673]
* Fixed localizable UI Automation Provider name for DataGridView EditingPanel.
In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. [654115, System.Windows.Forms.Dll, Bug, Build:3673]
* Fixed DataGridView not sortable column announcement and providing item status to prevent exposing 'Not sorted' info and just be silent regarding the sorting status for such columns. 
> In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. 
> In order for an application that targets 4.8 to opt out from this change, use the following combination of switches:
    <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/> [661319, System.Windows.Forms.Dll, Bug, Build:3673]

## Workflow

* Fixed an accessibility problem that the warning icons on workflow activity designer is not accessible [407415, System.Activities.Presentation.dll, Bug, Build:3673]
* Fixed an accessibility problem to enable connector label reading on workflow designer [604810, System.Activities.Presentation.dll, Bug, Build:3673]
* Fixed a problem with Transaction.Current and remoting operations.
In some .NET Remoting scenarios, when using TransactionScopeAsyncFlowOption.Enabled, it was possible to have Transaction.Current reset to null after a remoting call. Sometimes this was due to the remoting lease lifetime expiring while the remoting call was outstanding (pre 4.7.2). And sometimes this occurred when the remoting call did not leave the caller's AppDomain (with 4.7.2).
  This is now fixed for the latter case (remoting in the same AppDomain).
  For the former case (lease lifetime expires), a new AppSetting for the configuration file has been introduced to allow the user to specify the lease lifetime of the object used for keeping track of Transaction.Current in the call context. The user should set this to the number of minutes of the longest expected remoting call.
  The AppSetting looks like this:
  <add key=""Transactions:ContextKeyRemotingLeaseLifetimeInMinutes"" value=""5""/>
  The value specifies the lease lifetime for the object, in minutes. [672774, System.Transactions.dll, Bug, Build:3673]"
* Fixed an accessibility problem to have navigation information for ExpandAll/CollapseAll ToggleButtons on workflow designer. [682170, System.Activities.Presentation.dll, Bug, Build:3673]

## WPF

* Fixed the issue of WPF Windows not scaling correctly. WPF windows that are parented under native HWND’s, including Windows Forms (using ElementHost), will correctly react to DPI changes and scale themselves appropriately when the dpiAwareness element in the application manifest is updated to “PerMonitorV2” value. [478267, PresentationCore.dll,wpfgfx_v0400.dll, Feature, Build:3673]
* Fixed a race condition where an external process (e.g. anti-virus scanner or search indexer) could block access to temporary files. [519951, PresentationCore.dll, PresentationFramework.dll, System.Speech.dll, Bug, Build:3673]
* Automation properties set on TextBoxes within a DatePicker are now announced correctly by 3rd-party screen readers. [619245, PresentationCore.dll, Bug, Build:3673]
* Improved reliability of WPF under certain situations and prevents hangs.[629025, wpfgfx_v0400.dll, Bug, Build:3673]
* Fixed a regression involving bindings to properties of type DataView or RelatedView.  In some cases the value gets GC'd prematurely, causing the bindings to sliently stop working. [636340, PresentationFramework-SystemData.dll, Bug, Build:3673]
* When WPF is run in Per-Monitor Aware mode, controls hosted within HwndHost are not sized correctly after DPI changes (for e.g., when moving applications from one monitor to another). This fix ensures that controls hosted so are sized appropriately. 
On .NET Framework Versions 4.7.2 and older, applications must opt in to enable the fix by setting the AppContext switch 
""Switch.System.Windows.DoNotUsePresentationDpiCapabilityTier2OrGreater"" to ""false"". This switch can be set either in the registry or in the application - see the documentation for AppContext (https://msdn.microsoft.com/en-us/library/system.appcontext(v=vs.110).aspx). [646805,  PresentationFramework.dll;PresentationCore.dll;WindowsBase.dll, Bug, Build:3673]
* Fixed an issue arising when refreshing a grouped collection view.  While the groups are being rebuilt, they pass through a transient state where the subgroups are empty but the cached value for count still reports non-empty.   A re-entrant call to get an item at a given index during this time will get ArgumentOutOfRangeException, even though index < count. [656948, PresentationFramework.dll, Bug, Build:3673]
* Fixed a crash due to TaskCanceledException that can occur during shutdown of some WPF apps.   Apps that continue to do work involving weak events or data binding after Application.Run() returns are known to be vulnerable to this crash. [668328,WindowsBase.dll, Bug, Build:3673]
