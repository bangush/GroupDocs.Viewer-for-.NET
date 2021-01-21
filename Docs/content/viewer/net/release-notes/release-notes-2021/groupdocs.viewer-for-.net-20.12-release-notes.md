---
id: groupdocs-viewer-for-net-21-1-release-notes
url: viewer/net/groupdocs-viewer-for-net-21-1-release-notes
title: GroupDocs.Viewer for .NET 21.1 Release Notes
weight: 120
description: "Features, improvements, and bugs-fixes that are shipped in GroupDocs.Viewer for .NET 21.1"
keywords: release notes, groupdocs.viewer, .net, 21.1
productName: GroupDocs.Viewer for .NET
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Viewer for .NET 21.1{{< /alert >}}

## Major Features  

There are ? features, improvements, and bug-fixes in this release, most notable are:

* Item 1
* Item 2 
* Item 3

## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
|VIEWERNET-|Description|Feature|

## Public API and Backward Incompatible Changes

### Public API Changes

In this version we've simplified public API and added eight new constructors to the [Viewer](<https://apireference.groupdocs.com/viewer/net/groupdocs.viewer/viewer>) class that accept _Stream_ instead of _Func\<Stream\>_. The constructors that accept _Func\<Stream\>_ has been marked as obsolete, so please switch to the new constructors as we're planning to remove obsolete one in the future versions.

```csharp
// The following constructors has been added
public Viewer(Stream stream)
public Viewer(Stream stream, bool leaveOpen)
public Viewer(Stream stream, LoadOptions loadOptions)
public Viewer(Stream stream, LoadOptions loadOptions, bool leaveOpen)
public Viewer(Stream stream, ViewerSettings settings)
public Viewer(Stream stream, ViewerSettings settings, bool leaveOpen)
public Viewer(Stream stream, LoadOptions loadOptions, ViewerSettings settings)
public Viewer(Stream stream, LoadOptions loadOptions, ViewerSettings settings, bool leaveOpen)

// The following constructors were marked as obsolete
public Viewer(Common.Func<Stream> getFileStream)
public Viewer(Common.Func<Stream> getFileStream, Common.Func<LoadOptions> getLoadOptions)
public Viewer(Common.Func<Stream> getFileStream, ViewerSettings settings)
public Viewer(Common.Func<Stream> getFileStream, Common.Func<LoadOptions> getLoadOptions, ViewerSettings settings)
```
