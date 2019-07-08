# Geta Tags for EPiServer

![](<http://tc.geta.no/app/rest/builds/buildType:(id:TeamFrederik_Tags_TagsDebug)/statusIcon>)
[![Platform](https://img.shields.io/badge/Platform-.NET%204.6.1-blue.svg?style=flat)](https://msdn.microsoft.com/en-us/library/w0x726c2%28v=vs.110%29.aspx)
[![Platform](https://img.shields.io/badge/EPiServer-%2011-orange.svg?style=flat)](http://world.episerver.com/cms/)

## Description

Geta Tags is a library that adds tagging functionality to EPiServer content.

## Features

- Define tag properties
- Query for data
- Admin page for managing tags
- Tags maintenance schedule job

## How to get started?

Start by installing NuGet package (use [EPiServer NuGet](http://nuget.episerver.com/)):

    Install-Package Geta.Tags

The latest version is compiled for .NET 4.6.1 and EPiServer 11.
Geta Tags library uses [tag-it](https://github.com/aehlke/tag-it) jQuery UI plugin for selecting tags.
To add Tags as a new property to your page types you need to use the UIHint attribute like in this example:

```csharp
[UIHint("Tags")]
public virtual string Tags { get; set; }

[TagsGroupKey("mykey")]
[UIHint("Tags")]
public virtual string Tags { get; set; }

[CultureSpecific]
[UIHint("Tags")]
public virtual string Tags { get; set; }
```

Use ITagEngine to query for data:

```csharp
IEnumerable<ContentData> GetContentByTag(string tagName);
IEnumerable<ContentData> GetContentsByTag(Tag tag);
IEnumerable<ContentData> GetContentsByTag(string tagName, ContentReference rootContentReference);
IEnumerable<ContentData> GetContentsByTag(Tag tag, ContentReference rootContentReference);
IEnumerable<ContentReference> GetContentReferencesByTags(string tagNames);
IEnumerable<ContentReference> GetContentReferencesByTags(IEnumerable<Tag> tags);
IEnumerable<ContentReference> GetContentReferencesByTags(string tagNames, ContentReference rootContentReference);
IEnumerable<ContentReference> GetContentReferencesByTags(IEnumerable<Tag> tags, ContentReference rootContentReference);
```

##Customize Tag-it behaviour
You can customize the [Tag-it.js](https://github.com/aehlke/tag-it) settings by using the GetaTagsAttribute.
The following settings can currently be customized

- allowSpaces - defaults to **false**
- allowDuplicates - defaults to **false**
- caseSensitive - defaults to **true**
- readOnly - defaults to **false**
- tagLimit - defaults to **-1** (none)

```csharp
[CultureSpecific]
[UIHint("Tags")]
[GetaTags(AllowSpaces = true, AllowDuplicates = true, CaseSensitive = false, ReadOnly = true)]
public virtual string Tags { get; set; }
```

## Local development setup

In order to debug or contribute to the package, the Alloy demo site which is included in the repository can be used.

### Prerequisites

- Checkout the repository
- Install Docker on your local machine: https://docs.docker.com/get-started/
- [Optional] Install the Docker extension for Visual Studio

### Get started

Set the `docker-compose` as default project (if not already by default). Now, the required images are downloaded (windows server and sql server), this will take some time. Note, that this is only needed once. See Output window (source Docker) to follow the progress.

![Docker output](docs/images/docker-output.PNG)

After the images are downloaded just run the project and start debugging the code. The frontend and backend code can be found in the Geta.Tags project. The frontend code is available under the module folder.

### Alloy login

Use the default epiadmin user for Alloy, see [logins](https://github.com/episerver/AlloyDemoKit/wiki/Logins).

## Package maintainer

https://github.com/patkleef

## Changelog

[Changelog](CHANGELOG.md)
