# OpenApi3 Sample - Petstore

This is a quick start quick on how to generate the petstore openapi spec using a dotnet core project file

## Please execute the following from the directory where the project.csproj file is located

Install NPM Packages
```
npm install
```
Restore Nuget Packages for Project

```
dotnet restore
```

Build Project
```
dotnet build
```

This will generate the code from the openapi yml file located under 
```
./petstoredoc/petstore.yml
```

Generated output files/project will be located under

```
./petstorecodegen
```

Move to Petsore.Server.Api

```
cd ./petstorecodegen
```

Manual Fixes for Generated Code
 - (Fix missing ";,]["  and await async task to await task in partial or abstract classes generated )

1. Open ./petstorecodegen/src/Petsore.Server.Api/Startup.cs
```
close off "services.AddAuthorization" with "});"
```
2. Open ./petstorecodegen/src/Petsore.Server.Api/Authentication/ApiAuthentication.cs
```
close off "if (context.Resource  is  AuthorizationFilterContext  authorizationFilterContext)" with "}"
```
3. Search for "abstract async Task"
```
replace with "abstract Task"
```

Restore and build:

```
Windows: ./build.bat

Linux: ./build.sh
```

Run:
```
dotnet run -p src\Petsore.Server.Api\Petsore.Server.Api.csproj
```

Test Swagger:
```
Open browser and navigate to [http://localhost:8080/swagger](http://localhost:8080/swagger)
```

## Installing openapi-generate-cli globally

```
npm install @openapitools/openapi-generator-cli -g
```
Alternatively see [OpenAPI Generator Installation](https://openapi-generator.tech/docs/installation)

## serverConfig.json Options

openapi-generate-cli config options for aspnetcore

Run the following to see config options:
```
openapi-generator config-help -g aspnetcore
```
Output:

```
CONFIG OPTIONS
        licenseUrl
            The URL of the license (Default: http://localhost)

        licenseName
            The name of the license (Default: NoLicense)

        packageCopyright
            Specifies an AssemblyCopyright for the .NET Framework global assembly attributes stored in the AssemblyInfo file. (Default: No Copyright)

        packageAuthors
            Specifies Authors property in the .NET Core project file. (Default: OpenAPI)

        packageTitle
            Specifies an AssemblyTitle for the .NET Framework global assembly attributes stored in the AssemblyInfo file. (Default: OpenAPI Library)

        packageName
            C# package name (convention: Title.Case). (Default: Org.OpenAPITools)

        packageVersion
            C# package version. (Default: 1.0.0)

        packageGuid
            The GUID that will be associated with the C# project

        sourceFolder
            source folder for generated code (Default: src)

        compatibilityVersion
            ASP.Net Core CompatibilityVersion (Default: Version_2_2)

        aspnetCoreVersion
            ASP.NET Core version: 3.0 (preview4 only), 2.2, 2.1, 2.0 (deprecated) (Default: 2.2)

        swashbuckleVersion
            Swashbucke version: 3.0.0, 4.0.0 (Default: 3.0.0)

        sortParamsByRequiredFlag
            Sort method arguments to place required parameters before optional parameters. (Default: true)

        useDateTimeOffset
            Use DateTimeOffset to model date-time properties (Default: false)

        useCollection
            Deserialize array types to Collection<T> instead of List<T>. (Default: false)

        returnICollection
            Return ICollection<T> instead of the concrete type. (Default: false)

        useSwashbuckle
            Uses the Swashbuckle.AspNetCore NuGet package for documentation. (Default: true)

        isLibrary
            Is the build a library (Default: false)

        useFrameworkReference
            Use frameworkReference for ASP.NET Core 3.0+ and  PackageReference  ASP.NET Core 2.2 or earlier. (Default: false)

        useNewtonsoft
            Uses the Newtonsoft JSON library. (Default: true)

        newtonsoftVersion
            Version for Microsoft.AspNetCore.Mvc.NewtonsoftJson for ASP.NET Core 3.0+ (Default: 3.0.0-preview5-19227-01)

        useDefaultRouting
            Use default routing for the  ASP.NET Core version. For 3.0 turn off default because it is not yet supported. (Default: true)

        classModifier
            Class Modifier can be empty, abstract (Default: )

        operationModifier
            Operation Modifier can be virtual, abstract or partial (Default: virtual)

        buildTarget
            Target to build an application or library (Default: program)

        generateBody
            Generates method body. (Default: true)

        operationIsAsync
            Set methods to async or sync (default). (Default: false)

        operationResultTask
            Set methods result to Task<>. (Default: false)

        modelClassModifier
            Model Class Modifier can be nothing or partial (Default: partial)
```