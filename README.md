# reniffects

reniffects is a single-page portfolio built with ASP.NET Core MVC (.NET 9) to showcase VFX direction work, film projects, and brand collaborations. The page uses a video-driven hero, neon-inspired styling, and responsive Razor views to present static content and media hosted in `wwwroot`.

## Features
- Autoplaying hero background video with headline and smooth scroll CTA.
- Sections for About, Visual Portfolio, Film Projects, Brand Collaborations (flip cards), and a Contact form stub.
- Responsive navigation with a mobile hamburger toggle and animated buttons.
- Local images, logos, and a hero video served from `wwwroot`.
- Minimal server-side code: a single `HomeController` and Razor views.

## Project layout
- `reniffects.sln` – solution entry point.
- `reniffects/Program.cs` – application bootstrap and routing.
- `reniffects/Controllers/HomeController.cs` – routes the home, privacy, and error pages.
- `reniffects/Views/Home/Index.cshtml` – main one-page layout with all sections.
- `reniffects/Views/Shared/_Layout.cshtml` – global shell, navbar, and footer.
- `reniffects/wwwroot/css/site.css` – custom styling; also contains all responsive rules.
- `reniffects/wwwroot/images`, `reniffects/wwwroot/videos` – media assets referenced by the page.
- `reniffects/Dockerfile` – Windows container image definition (Nano Server 1809).

## Prerequisites
- [.NET 9 SDK](https://dotnet.microsoft.com/download)
- (Optional) Docker with Windows containers enabled for the provided Nano Server image.

## Run locally
From the repository root:
1) Restore packages  
`dotnet restore reniffects/reniffects.csproj`
2) Run the app (Kestrel defaults to http://localhost:5000 and https://localhost:5001)  
`dotnet run --project reniffects/reniffects.csproj`

For hot reload during UI edits:  
`dotnet watch run --project reniffects/reniffects.csproj`

If you need full exception details, set the environment before running:  
`$env:ASPNETCORE_ENVIRONMENT = "Development"`

## Publish
Generate a self-contained release build to `./publish`:
`dotnet publish reniffects/reniffects.csproj -c Release -o ./publish`

## Docker (Windows containers)
The Dockerfile targets `mcr.microsoft.com/dotnet/aspnet:9.0-nanoserver-1809`, so ensure Windows container mode is enabled. Build and run from the repo root:
```
docker build -t reniffects -f reniffects/Dockerfile .
docker run -p 8080:8080 reniffects
```

## Notes and customization
- Media paths are hardcoded in `Views/Home/Index.cshtml`; place replacements in `wwwroot/images` and `wwwroot/videos` to avoid broken assets.
- The contact form is a static UI only; wire it up to an API or email service as needed.
- Styling lives in `wwwroot/css/site.css`; adjust the neon palette, typography, or layout there.
