---
title: Environments and Modes
---

# Environments and Modes

1. **`import.meta.env`:** A special object for accessing environment variables.
2. **`.env` Files:** Used to define environment variables.
3. **Modes:** Development, production, etc., to manage multiple environment setups.
4. **TypeScript IntelliSense:** Autocompletion for custom variables.
5. **HTML Env Replacement:** Using env variables in HTML files.
6. **Security Considerations:** Warnings about sensitive data.

## `import.meta.env`

- **Built-in Variables:**
  - `MODE`: Running mode (development, production, etc.)
  - `BASE_URL`: Base URL of the app
  - `PROD`: Boolean, indicating if in production
  - `DEV`: Boolean, indicating if in development
  - `SSR`: Boolean, indicating if in server-side rendering mode
- **Production Replacement:** In production, these variables are statically replaced. Special consideration is needed for dynamic key access and Vue templates.

## `.env` Files

- **Loading Mechanism:** Uses `dotenv` and `dotenv-expand` libraries to load variables from `.env` files located in a specific directory.
- **Files:**
  - `.env`: Loaded always
  - `.env.local`: Loaded always, ignored by git
  - `.env.[mode]`: Loaded in a specified mode
  - `.env.[mode].local`: Loaded in a specified mode, ignored by git
- **Priority:**
  - Variables existing at the time of Vite execution take the highest priority.
  - Specific mode files override generic ones.
- **Security:**
  - Only variables prefixed with `VITE_` are exposed to the client.
  - Sensitive information should not be included.

## TypeScript IntelliSense

- Custom `.d.ts` file can be created to provide TypeScript autocompletion for custom variables prefixed with `VITE_`.

## HTML Env Replacement

- Variables can be used in HTML files using `%ENV_NAME%` syntax.

## Modes

- `development` for dev server and `production` for build command, by default.
- Modes determine which `.env` files get loaded.
- Command-line flag `--mode` can be used to specify a mode.

## Security Notes

- `.env.*.local` files are local-only and should not be checked into version control.
- No sensitive data should be prefixed with `VITE_` as it will be exposed to the client.
