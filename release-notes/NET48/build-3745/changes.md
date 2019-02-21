# .NET Framework Build 3745 Release Notes
Following changes are included in .NET Framework 4.8 build 3745. You can view the full list of [.NET Framework 4.8 Changes](/release-notes/NET48/dotnet-48-changes.md) (all changes, including those in build 3745 and builds upto current date).

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## BCL

Added support for formatting the Japanese first year of era using Gannen 元 when the date pattern not having single quotes around 年. e.g. y年. [777279, mscorlib.dll, Bug, Build:3745]

## Networking

* Fixed domain spoofing vulnerability in .NET Framework and .NET Core which causes the meaning of a URI to change when International Domain Name encoding is applied by disallowing certain Unicode characters during the IDN encoding process - CVE-2019-0657 [694688, System.Private.Uri, Bug, Build:3745]

## WCF

* Made some format changes and added lang attribute to WCF service Health page (like http://localhost:83/Service1?health) and WCF service metadata page (like http://localhost:83/Service1) to improve accessibility. [777308, System.ServiceModel.dll, Bug, Build:3745]

## WorkFlow

* Fixed a vulnerability in the WorkflowMarkupSerializer that allowed "random" code to be executed with certain XOML constructs.
If users experience application compatibility problems, there are couple of "opt-out" < appSettings> values that allow users to modify the behavior introduced by this change:
```xml
<add key="microsoft:WorkflowComponentModel:DisableXOMLSerializerTypeChecking" value="true"/>
```
Setting this value to "true" completely disables the type checking that is done during deserialization. It takes precedence over the value below.
```xml
<add key="microsoft:WorkflowComponentModel:DisableXOMLSerializerDefaultUnauthorizedTypes" value="true"/>
```
The type checker has a list of hard-coded types that are disallowed by default. Setting this value to "true" allows those hard-coded types. The user can specify a list of unauthorized types on their own by adding the following to the app.config file:
```xml
<configuration>
  <configSections>​
    <sectionGroup name="System.Workflow.ComponentModel.WorkflowCompiler" type="System.Workflow.ComponentModel.Compiler.WorkflowCompilerConfigurationSectionGroup, System.Workflow.ComponentModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35">​
      <section name="authorizedTypes" type="System.Workflow.ComponentModel.Compiler.AuthorizedTypesSectionHandler, System.Workflow.ComponentModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>​
    </sectionGroup>​
  </configSections>​

<System.Workflow.ComponentModel.WorkflowCompiler>
    <authorizedTypes>​
      <myAuthorizedTypes version="v4.0">​
        <authorizedType Assembly="System.Activities.Presentation, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" Namespace="System.Activities.Presentation" TypeName="WorkflowDesigner" Authorized="false"/>
      </myAuthorizedTypes>
    </authorizedTypes>​
  </System.Workflow.ComponentModel.WorkflowCompiler>​
</configuration>
```

In the above example, the type System.ActivitiesPresentation.WorkflowDesigner in the System.Activities.Presentation assembly is unauthorized because its "Authorized" value is "false". [735532, System.Workflow.ComponentModel.dll, Bug, Build:3745]

## WPF

* Added an AppContext switch 'Switch.System.Windows.Controls.ItemsControlDoesNotSupportAutomation' that guards the fix for the automation tree under a plain ItemsControl (previously disclosed Bug 410007).  This switch defaults to 'false' for apps that target .NET 4.8, or to 'true' for apps that target earlier versions.   [778689, PresentationCore.dll, WindowsBase.dll, Bug, Build:3745]
