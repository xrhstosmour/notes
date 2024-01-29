#application #dotnet #packages

1. **Create an .NET application template**

   - **Console Application:**

``` bash
dotnet new console -o <ApplicationName>
```

   - **.NET Minimal API with Controllers:**

``` bash
dotnet new webapi --use-controllers -o <ApplicationName>
```

   - **ASP.NET Core Web Application (MVC):**

``` bash
dotnet new mvc -o <ApplicationName>
```

   - **Class Library:**

``` bash
dotnet new classlib -o <LibraryName>
```

   - **ASP.NET Core Web Application (Razor Pages):**

``` bash
dotnet new razor -o <ApplicationName>
```

   - **Blazor Server App:**

``` bash
dotnet new blazorserver -o <ApplicationName>
```

   - **Blazor WebAssembly App:**

``` bash
dotnet new blazorwasm -o <ApplicationName>
```

   - **Angular Application:**

``` bash
dotnet new angular -o <ApplicationName>
```

2. **Trust the self-signed certificate**

``` bash
dotnet dev-certs https --trust
```

3. **Add possible packages**

``` bash
dotnet add package <PackageName>
```

4. **Add .gitignore**

``` bash
dotnet new gitignore
```
