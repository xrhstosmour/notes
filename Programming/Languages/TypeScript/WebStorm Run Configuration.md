#typescript #webstorm #nodejs #run-configuration

Setting up a Node.js/TypeScript project to run and compile from WebStorm:

1. Install Node.js, npm, and `typescript` globally or as a dev dependency.
2. Add a Node.js run configuration pointing at the app's entry point, e.g. `bin/www` for an Express-style app.
3. Add a "Compile TypeScript" step as a **Before launch** task on that run configuration, so `tsc` runs automatically before each start.
4. Run `npm install` once to pull in project dependencies before the first run.
