# .NET Framework Build 3646 Release Notes
Following changes are included in .NET Framework 4.8 build 3646. You can view the full list of [.NET Framework 4.8 Changes](/release-notes/NET48/dotnet-48-changes.md) (all changes, including those in build 3646 and builds upto current date).

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## BCL

* Fixed the serialization compatibility issue for CultureAwareComparer class. [621387, mscorlib.dll , Bug, Build:3632]

## CLR

* The ‘shadowCopyVerifyByTimestamp’ setting is now configurable for individual appdomains, as opposed to being a process wide setting.  This helps in situations where you may not be the host process, but want to configure a new appdomain that verifys timestamps when shadow copying. [565570, clr.dll, Bug, Build:3632]

## SQL

* Fixed the following issue relevant to SQL: while connecting to Azure SQL DB using .NET 4.7.2, using MultipleActiveResultSets=true in the connection string with System.Data.SqlClient.SqlConnection, async query operations sometimes lead to a bad TDS protocol request stream to be sent from the client, causing the Async Query APIs to fail connection string. [624283, System.Data.dll, Bug, Build:3632]

## Windows Forms

* Added support for UIA notification event to ProgressBar class. The feature is available starting with Windows 10, version 1709 (RS3). [581351, System.Windows.Forms.dll, Bug, Build:3632]
* Fixed an issue where read-only Status for DataGridView TextBox column is not announced by Narrator. This change is effective in applications that were recompiled to target .NET framework 4.8. [599936, System.Windows.Forms.dll, Bug, Build:3632]
* Fixed reliability issues in Graphics class when used in RDP sessions. [627739, System.Drawing.dll, Bug, Build:3632]

## WPF

* Fixed incorrect result of pressing an arrow key when focus is on a Hyperlink within an item that is not the SelectedItem of the parent ItemsControl. [405208, PresentationFramework.dll, Bug, Build:3646]
* Fixed incorrect result of pressing an arrow key when focus is on a Hyperlink within an item that is not the SelectedItem of the parent ItemsControl. [405208, PresentationFramework.dll, Bug, Build:3646]
* Fixed issue of internal class protector returning wrong order. [442569, PresentationCore.dll, Bug, Build:3646]
* Fixed usage of resources internal to theme files to avoid potential conflicts. [494194, System.Windows.Controls.Ribbon.dll, Bug, Build:3646]
* Fixed an issue where automation properties set on an editable RibbonComboBox  are not properly announced by screen readers or other assistive technologies. [520147, PresentationCore.dll, Bug, Build:3646]
* GridViews with focusable Header rows will now not experience keyboard focus landing on the padding column in the header. [559546, PresentationFramework.dll, Bug, Build:3646]
* Fixed Binding's incorrect use of IList indexer when the source object declares a custom indexer with the same signature  [585942, PresentationFramework.dll, Bug, Build:3646]
* Fixed the issues of certain bounding rectangles, not being drawn corrently. When WPF is run in Per-Monitor Aware mode, certain bounding rectangles around text are drawn incorrectly by Accessibility tools like Narrator. This fix addresses the problem. To opt-into this fix, the target framework version of the Application should be set to .NET 4.8. Alternatively, an AppContext switch - "Switch.UseLegacyAccessibilityFeatures.2" - can be overridden with the value "false" to enable the fix.  [617457, PresentationFramework.dll, Bug, Build:3646]
* Fixed a hang arising during layout of a Grid when UseLayoutRounding=true, high DPI is in effect, grid *-column widths are determined from children with ColumnSpan > 1, and floating-point roundoff is unfavorable. [619978, PresentationFramework.dll, Bug, Build:3646]
* Fixed an issue where re-entrant calls during shutdown could cause various application faults in WPF applications running on a touch or stylus enabled machine. [633620, PresentationCore.dll, PresentationFramework.dll, Bug, Build:3646]
* Fixed a memory leak arising when the number of TextBoxes drops to 0. [645497, PresentationFramework.dll, Bug, Build:3646]
* Fixed the DeadLock issue faced during creation of Spellchecker while Finalizer is ending another Instance. Under certain circumstances, WPF applications using the spell-checker that use custom dictionaries could throw unexpected excpetions and crash [646599, PresentationFramework.dll, Bug, Build:3646]
* Addressed the issue where GroupItem headers containing an Expander were not announced correctly by screen readers [646633, PresentationFramework.dll, Bug, Build:3646]
* Fixed WPF issue of not creating correctly-size rendertarget for mixed-mode child windows. Under certain circumstances, per-monitor DPI aware applications that host WPF based controls or plugins were not rendering the WPF window fully [646801, wpfgfx_v0400.dll, Bug, Build:3646]
* Addressed the restore issue of Window.Left & Window.Top. When WPF applications are running in per-monitor aware mode, saving the value of Window.Left and Window.Top at application end, and restoring the values to a Window prior to creation upon the next application launch, was not restoring the application to the same screen position where it was at the time the application was closed. [646803, PresentationFramework.dll;PresentationCore.dll;WindowsBase.dll, Bug, Build:3646]
* Fixed the issue where HwndHost does not adapt child-HWND sizing correctly during DPI changes. When WPF is run in Per-Monitor Aware mode, controls hosted within HwndHost were not sized correctly after DPI changes (for e.g., when moving applications from one monitor to another). This fix ensures that controls hosted so are sized appropriately [646805, PresentationFramework.dll;PresentationCore.dll;WindowsBase.dll, Bug, Build:3646]