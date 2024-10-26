<!-- #resources -->

This package generates a static `ThisAssembly.Resources` class with public
properties exposing typed APIs to retrieve the contents of embedded resources.


```xml
  <ItemGroup>
    <EmbeddedResource Include="Content/Docs/License.md" />
  </ItemGroup>
```

![](https://raw.githubusercontent.com/devlooped/ThisAssembly/main/img/ThisAssembly.Resources.png)

Since markdown files are text files, the API will expose a `Text` property property
for it that will read its content once and cache it:

![](https://raw.githubusercontent.com/devlooped/ThisAssembly/main/img/ThisAssembly.Resources2.png)

The `$(EmbeddedResourceStringExtensions)` MSBuild property allows customizing which
file extensions get treated as text files. By default, it's defined as:

```xml
  <PropertyGroup>
    <EmbeddedResourceStringExtensions>.txt|.cs|.sql|.json|.md</EmbeddedResourceStringExtensions>
  </PropertyGroup>
```

You can append additional file extensions to this list, or override it completely.
The list must be pipe-separated.

You can always use the provided `GetStream` and `GetBytes` for more advanced scenarios (or for
non-text resources).

Optionally, you can specify the `Kind` metadata for a specific `EmbeddedResource` you want
treated as a text file:

```xml
    <EmbeddedResource Include="query.kql" Kind="Text" />
```

You can also add a `Comment` item metadata attribute, which will be used as the `<summary>` XML
doc for the generated member.

## Customizing the generated code

The following MSBuild properties can be used to customize the generated code:

| Property                | Description                                                                                          |
|-------------------------|------------------------------------------------------------------------------------------------------|
| ThisAssemblyNamespace   | Sets the namespace of the generated `ThisAssembly` root class. If not set, it will be in the global namespace. |
| ThisAssemblyVisibility  | Sets the visibility modifier of the generated `ThisAssembly` root class. If not set, it will be internal. |

<!-- #resources -->
<!-- exclude -->