#typescript #release #build #deployment

1. Compile: `tsc`
2. Package only what the running app needs, not the whole repo, a typical Node/TypeScript web app release includes:
   - `bin/` (entry point)
   - `dist/` (compiled JS output)
   - `config/`
   - `public/`
   - `views/`
   - `package.json` (and `package-lock.json`)
   - `web.config` (if hosted on IIS, see [[Enable SSL for IIS Express]] for local IIS Express testing)
3. Leave out `src/`, test files, and dev-only tooling from the release artifact.
