#application #dotnet #packages

1. **Create an .NET application template**

   - **Console Application**: `dotnet new console -o <ApplicationName>`

   - **.NET Minimal API with Controllers**: `dotnet new webapi --use-controllers -o <ApplicationName>`

   - **ASP.NET Core Web Application (MVC)**: `dotnet new mvc -o <ApplicationName>`

   - **Class Library**: `dotnet new classlib -o <LibraryName>`

   - **ASP.NET Core Web Application (Razor Pages)**: `dotnet new razor -o <ApplicationName>`

   - **Blazor Server App**: `dotnet new blazorserver -o <ApplicationName>`

   - **Blazor WebAssembly App**: `dotnet new blazorwasm -o <ApplicationName>`

   - **Angular Application**: `dotnet new angular -o <ApplicationName>`

2. **Trust the self-signed certificate** `dotnet dev-certs https --trust`

3. **Add possible packages** `dotnet add package <PackageName>`

4. **Add .gitignore** `dotnet new gitignore`
