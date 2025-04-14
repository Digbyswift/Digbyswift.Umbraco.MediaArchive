# Digbyswift.Umbraco.MediaArchive

[![NuGet version (Digbyswift.Umbraco.MediaArchive)](https://img.shields.io/nuget/v/Digbyswift.Umbraco.MediaArchive.svg)](https://www.nuget.org/packages/Digbyswift.Umbraco.MediaArchive/)
[![Build Status](https://dev.azure.com/digbyswift/Digbyswift%20-%20NuGet%20Packages/_apis/build/status%2FDigbyswift.Umbraco.MediaArchive?branchName=master)](https://dev.azure.com/digbyswift/Digbyswift%20-%20NuGet%20Packages/_build/latest?definitionId=57&branchName=master)

Forces 404 status codes for recycled media in Umbraco.

## Why?

In Umbraco, when a media item is moved to the recycle bin, the physical media is still available at the media item's URL.

This means that:

1. Recycled media can't be tracked by running broken link checkers on the front end;
2. Redirects created in packages like Skybrud.Redirects will not work on recycled media because they rely on the request returning a 404.

This package will force the media to return a 404 once moved to the recycle bin.

## How?

It does this by moving media to a separate `/_archive/` folder and then restoring the media to it's original folder if restored from the recycle bin.

## Setup

Include the `AddMediaArchive()` extension method in the startup of the project:

```csharp
var umbracoBuilder = builder
    .CreateUmbracoBuilder()
    .AddBackOffice()
    .AddWebsite()
    .AddComposers()
    .AddMediaArchive()
```


## Config

By default the package is enabled, but you can disable it using the following config setting:

```json
{
  "Digbyswift": {
    "MediaArchive": {
      "Enabled": false
    }
  }
}
```
