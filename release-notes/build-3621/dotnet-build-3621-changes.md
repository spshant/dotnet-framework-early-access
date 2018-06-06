# .NET Framework Build 3621 Release Notes

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## BCL

* Fixed deserialization of Collections which uses culture aware StringComparer. [566534, mscorlib.dll, Bug]
* Fixed System.Runtime.CompilerServices.RuntimeFeature.IsSupported to correctly account for application compatibility quirk settings for the Portable PDB feature introduced in .NET Framework 4.7.1. [571206, mscorlib.dll, Bug]
* Fixed the exception by parsing Japanese dates that have the year number exceeding the number of years in that date era. The behavior change will be noticed only if someone tries to parse a date containing some era and year while the year exceeds the last year in that era. [590659, mscorlib.dll, Bug]
* By default, elevated processes will not read HKCU for managed COM activation information. [592187, clr.dll, Bug]

## ClickOnce

* Fixed Clickonce UI dialogs on high Dpi machines with scale set to more than 100% for both new and existing applications which scale upto 300%. In the scenario where user wants to see legacy images, there is an opt out switch "Switch.System.Windows.Forms.UseLegacyImages" that can be set to "true" in dfsvc.exe.config file. [389534, Microsoft.Build.Tasks.v4.0.dll, Bug]
* Fixed Mage so it can properly update the identity of dependent assemblies in ClickOnce application manifests. [534286, Microsoft.Build.Tasks.v4.0.dll, Bug]
* Fixed ClickOnce dialogs (Splash screen, Install progress dialog, Maintenance dialog and Update dialog) have accessibility issues as mentioned in this bug. Fix is for realigning control indices and setting accessible names where it was missing. [541886, Microsoft.Build.Tasks.v4.0.dll, Bug]
* Fixed progress bar alignment from Right to Left in Splash Screen and Download progress dialog for ARA & HEB languages for ClickOnce UI. Fixed RTL layout in the ClickOnce dialogs. Individual controls are to be set in RTL layout as this property is not propagated. Set this property explicitly on progress bar control.[552893, Microsoft.Build.Tasks.v4.0.dll, Bug]

## CLR

* Fixed LoadFrom(String, Byte[], AssemblyHashAlgorithm) works with SHA2 algorithms. [229901, mscorlib.dll, Bug]
* Reduced AsyncLocal memory overhead on value change. [470761, mscorlib.dll, Bug]
* Improved spin-waits in several synchronization primitives to perform better on Intel Skylake and more recent microarchitectures. [495945, mscorlib.dll, Bug]
* Fixed issues where incorrect values are sent to EventListeners.  This includes incorrect activity ids on start and stop events and improper EventLevel values. [581072, mscorlib.dll, Bug]
* Fixed a potential crash with concurrent calls to a new dynamic method. [581154, mscorlib.dll, Bug]
* Fixed a possible deadlock when calling Dispose() on an EventSource. [597221, System.Core.dll, Bug]

## Networking

* Fixed a memory leak issue in HttpWebRequest when communicating with a HTTPS server through a proxy. [484621, System.dll, Bug]
* Fixed HTTP Status line parsing to be more tolerant of missing status description text in HTTP responses. [534936, System.dll, Bug]
* Fixed a NetworkInformation.NetworkChange deadlock scenario when there is a lock around NetworkChanged listener and user’s callback. [554780, System.Net.NetworkInformation.dll, System.dll, netstandard.dll, Bug]

## SQL

* Fixed the issue that SqlDataReader.ReadAsync() runs synchronously. Now the method runs asynchronously as expected. [594433, System.Data.dll, Bug]
* Fixed the issue while using SqlConnection.ConnectionString to set a null or empty connection string, an NRE exception will be thrown by the usage of the API in .Net Framework 4.7.2. [613944, System.Data.dll, Bug]

## WCF

* Fixed an accessibility problem in WCF Trace Viewer that caused ComboBox controls to be themed incorrectly in High Contrast themes. [424922, SvcTraceViewer.exe, Bug]
* Fixed the race-condition that exists in AsyncResult that closes a WaitHandle before Set() is called. When this happens, the process crashes with an ObjectDisposedException. [552736, System.ServiceModel.Internals.dll, Bug]
* Fixed race-condition when aborting connections which caused ObjectDisposedException to be thrown in CleanupChannelCollections. [586151, mscorlib.dll, Bug]

## Windows Forms

* Enabled labels are now always rendered using a high contrast text color when a high contrast mode is enabled. This change is effective in applications that are recompiled to target .NET Framework 4.8 [486578, System.Windows.Forms.dll, Bug]
* Maximize/Minimize button of new child Form are not scaled well on HDPI  devices because of image property set to not to scale. On 100% dpi machines scaling it not required but on high dpi devices, when scaling set to more than 100%, the images set for Maximize/Minimize boxes need to be scaled. [515092, System.Windows.Forms.dll, Bug]
* Checkbox height is changed from square to rectangle when scaled. Padding and margins were scaled, thus adding to already scaled height of the checkbox as we were using item height to draw checkbox instead of checkbox height. Earlier these margins/paddings were constants and ignorable pixel sizes, and were not visible. [528418, System.Windows.Forms.dll, Bug]
* The new UIA behavior for CheckedListBox control has been introduced: the first checkbox item in the CheckedListBox control is now announced by Narrator when focus moves to the control without any selected item. This change is effective in applications that were recompiled to target .NET Framework 4.8. [533226, System.Windows.Forms.dll, Bug]
* The new behavior for disabled link labels has been introduced: link labels' enable/disable state is now provided correctly - disabled links have IsEnabled = false Accessibility Property and read by Narrator as 'Some Link, disabled'. This change is effective in applications that were recompiled to target .NET Framework 4.8. [537224, System.Windows.Forms.dll, Bug]
* The new behavior for link label with defined link area has been introduced: link area accessible name is now read by Narrator as full text of the parent link label. This change is effective in applications that were recompiled to target .NET Framework 4.8. [537934, System.Windows.Forms.dll, Bug]
* Improved accessibility for the DateTimePicker control. In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. [543580, System.Windows.Forms.dll, Bug]
* An associated label name is now used as an accessible name for DateTimePicker control when AccessibleName property is not set. The default DateTimePicker's AccessibleRole is ComboBox now. These changes are effective in applications that were recompiled to target .Net Framework 4.8. [544791, System.Windows.Forms.dll, Bug]
* Fixed issues to add support for UIA live regions to WinForms. Added support for notifications about the Text property changes to the Label class (through UIA Live Regions). [545374, System.Windows.Forms.dll, Bug]
* Application Files' and 'Application Directory' label text is truncated on localized OSes. Developers will not be able to see the shortcut information for this control on the UI. This fix helps to resolve that issue and always show the full text of the label . [549024, System.Windows.Forms.dll, Bug]
* The new UIA behavior for numeric and domain up-down controls has been introduced: numeric and domain up-down controls without labels (custom UIA name) are announced by Narrator as 'spinners'. This change is effective in applications that were recompiled to target .NET Framework 4.8. [549543, System.Windows.Forms.dll, Bug]
* The new UIA behavior for CheckedListBox control has been introduced: an empty CheckedListBox control now has a focus rectangle drawn for a virtual first item when the control becomes focused. This change is effective in applications that were recompiled to target .NET Framework 4.8. [549558, System.Windows.Forms.dll, Bug]
* Improved ListView accessibility by enabling showing grey rectangle around the selected ListView item when parent ListView is out if focus. This change is effective in applications that were recompiled to target .NET Framework 4.8. [564762, System.Windows.Forms.dll, Bug]
* Fixed VisualStyle property in Winforms, is checking for supported values (by Winforms) and any value that goes outside of this range, Winforms throws an exception. Winforms also checks if the VisualStyle property set is supported by Winforms when it is using this property and does no-op if it is not supported. Underlying native method we use to set visual styles does not care what the value for visualstyle is being passed to it.  Making this change will align Winforms code with windows and does not throw exception but still validate supported visual styles when using this property. Removing the validation condition while setting this property. [578093, System.Windows.Forms.dll, Bug]
* Fixed the DataGridView's Combobox expand/collapse state accessible for the customers who use assistive technologies. In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>    
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/> [574309, System.Windows.Forms.dll, Bug]
* Fixed and improved the stability of Live Regions feature by adding LiveSetting property setter check. This feature is available starting with Windows 10, version 1709 (RS3).
In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/> [583863, System.Windows.Forms.dll, Bug]
* Fixed Winforms application and controls, when enable for ""per-Monitor"" Dpi aware, they are not scaled according to the dpi of the monitor ( or device). Winforms app by default behave like ""System"" Dpi aware. This is causing Winforms applications/controls to be displayed ""blur"" as a result of windows scaling them and in some cases, controls are either not scaled or scaled out of proportionate. Made changes on control level to respond to DPI change event (assuming  windows raise this event whenever there is a DPI change) and rescale controls according to the new DPI. [597091, System.Windows.Forms.dll, Bug]
* Fixed by adding support for UIA notification event to Label and GroupBox classes. This feature is available starting with Windows 10, version 1709 (RS3). In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/> [563596, Windows.UI.Xaml.Automation.Peers.dll, Windows.dll, Bug]
* Fixed by adding support for the live region feature to the ToolStripStatusLabel class. In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/> [564300,Windows.UI.Xaml.Automation.Peers.dll, Windows.dll, Bug]
* Fixed by improving the accessibility of DataGridView and ListView to make sort direction available via UIA: added exposing sort order and sort column via ItemStatus property and column name. This change is effective in applications that were recompiled to target .NET Framework 4.8. [549288, System.Windows.Forms.dll, Bug]
* Fixed by making the forward and backward toolstrip navigation consistent. This feature is available starting with Windows 10, version 1709 (RS3). In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/> [544592, System.Windows.Forms.dll, Bug]
* Fixed the announcement of DataGridView Read-only TextBox cells by making accessible and clear: editable TextBoxes are announced as 'editable' and read-only TextBoxes are announced as 'read-only'. This change is effective in applications that were recompiled to target .NET Framework 4.8. [599936, System.Windows.Forms.dll, Bug]

## WPF

* Fixed a memory leak arising when removing data items from their parent collections, when UIAutomation is present. [172291, PresentationFramework.dll, Bug]
* Fixed virtualizing ItemsControl hung during scrolling when Items collection contains duplicate value-typed objects. [360053, PresentationFramework.dll, Bug]
* Fixed WPF application can crash with NullReferenceException when changing a property used by a DataTrigger whose host element has been removed from the visual tree.  The crash only occurs if the host element is garbage-collected during a small window of time during the property-change notification. [401484, PresentationFramework.dll, Bug]
* Fixed WPF app that has multiple top-level windows in different threads that crashes during a theme change. [404464, PresentationFramework.dll, Bug]
* Fixed WPF applications running on touch or stylus-enabled machines can sometimes hang at startup or during connection of a tablet or stylus device. [474688, PresentationFramework.dll, Bug]
* Fixed focus issues in WPF applications running in high contrast themes, it can be difficult to distinguish when a TextBox, PasswordBox, or RichTextBox has focus. [486957, PresentationFramework.dll, Bug]
* Fixed WPF applications using DocumentViewer controls may see issues with the rendering of text selection graphics after a theme change. This change addresses that issue. [494408, PresentationFramework.dll, Bug]
* In WPF applications running on touch or stylus-enabled machines that set the AppContext switch "Switch.System.Windows.Input.Stylus.EnablePointerSupport" to true, StylusPlugins would not be properly unhooked when element properties were changed prior to the presentation source being set to null. This change fixes this issue. [500125, PresentationFramework.dll, Bug]
* Fixed an issue that caused XAML Browser Applications (XBAP’s) targeting .NET 3.5 to sometimes load using .NET 4.x runtime incorrectly. [560029, PresentationHost_v0400.dll, Bug]
* Fixed an infinite loop arising during layout of a Grid in some cases when *-columns with MinSize constraints consume all the available space. [560609, PresentationFramework.dll, Bug]
* Fixed WPF applications running under high contrast themes, the border color of a disabled TextBox, RichTextBox, and PasswordBox was incorrect. This change addresses that issue. [527669, PresentationFramework.dll, Bug]
* Fixed WPF applications using non-adorner based text selection for TextBox and PasswordBox (Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering=false), developers may now set the SelectionTextBrush property in order to alter the rendering of the selected text. By default, this color changes with SystemColors.HighlightTextBrushKey. If non-adorner based text selection is not enabled, this property does nothing. [531137, PresentationFramework.dll, Bug]
* Fixed WPF application running in high contrast mode has difficult to see selection visuals on DataGridCells. This change addresses that issue. [545871, PresentationFramework.dll, Bug]
* Fixed WPF applications running on a touch or stylus-enabled machine, users might periodically see a crash in System.Windows.Window.GetWindowMinMax. This change addresses that issue. [546769, PresentationFramework.dll, Bug]
* Fixed a memory leak arising when sending bitmaps to the clipboard. [589759, PresentationCore.dll, Bug]
* Fixed WPF application running on a stylus or touch-enabled machine may see NullReferenceExceptions or InvalidCastExceptions under certain circumstances. This change addresses this issue. [577690, PresentationCore.dll, Bug]
* Fixed issue when non-Adorner-based text selection is enabled in .NET Framework 4.7.2 and above, the default SelectionOpacity of FlowDocumentReader, FlowDocumentScrollViewer, and SinglePageViewer will cause the selection to obscure the underlying text. This change addresses this issue by setting the default SelectionOpacity to the correct value. [568305, PresentationFramework.dll, Bug]
* Fixed WPF applications using non-adorner based text selection (AppContext flag "Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering=false"), editable ComboBoxes do not appropriately follow theme colors for text selection. [572332, PresentationFramework.dll, Bug]
* Fixed timing issues in the finalizer thread could potentially cause exceptions during AppDomain or process shutdown in certain .NET applications. This is generally seen in applications that do not correctly shut down Dispatchers running on worker threads prior to process or AppDomain shutdown. Such applications should take care to properly manage the lifetime of Dispatchers. This change adds an AppContext switch that can help alleviate (but not eliminate) some of the issues that may arise from these application design issues. To enable this, set the AppContext flag "Switch.MS.Internal.DoNotInvokeInWeakEventTableShutdownListener=true". [606492, WindowsBase.dll, Bug]
* Fixed crash issues and allows the replace to proceed.When replacing multiple characters with a single character (in a different language than replaced text) using IMEPad, WPF crashes. [595046, PresentationFramework.dll, Bug]
* Fixed WPF application that changes TreeView.IsEnabled and (at the same time) changes the underyling collection(s) can experience a spurious ElementNotAvailableException. [573999, PresentationFramework.dll, Bug]

## WorkFlow

* We have modified the hashing algorithm used to generate XOML file checksums when building projects with XOML files. If this causes problems, the previous hashing algorithm can be used by specifying ""true"" for the following AppContext switch: Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum. Note that this AppContext switch applies to the MSBuild process, so must be specified in the ""config path"" of the MSBuild.Exe that is used to perform the builds. [531054, System.Workflow.Runtime.dll, Bug]
* We have modified the hashing algorithm used to calculate keys to internal in-memory caches. If this causes problems, the previous hashing algorithm can be used by specifying ""true"" for the following AppContext switches: Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey [532505, System.Workflow.Runtime.dll, Bug]"
* Fixed default hashing algorithm that help debugging symbols has changed. If you encounter problems with breakpoints in the workflow designer not being hit when expected, you may have a mismatch of hashing algorithms between MSBuild and the project being debugged. The following AppContext switch can be specified for MSBuild.exe and the project being debugged to help alleviate the problem. Switch.System.Activities.UseLegacyHashForDebuggerSymbols If this switch has a value of ""true"", then the default hashing algorithm for pre-4.7.2 versions of .NET are used. If the value of the switch is ""false"", the newer default hashing algorithm is used. [537692, System.Workflow.Runtime.dll, Bug]
* Previously, under extreme usage conditions (high volume of connections to MSDTC), it was possible for a CriticalSection to be held by a single thread indefinitely, resulting in the need to restart the process. This problem has been resolved. In addition, some object caches that would help performance in multi-threaded scenarios were not taken advantage of correctly. This has been resolved. [540812, System.Workflow.Runtime.dll, Bug]
