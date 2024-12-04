# React + Electron + TypeScript + Vite

This template is based on Vite React + TypeScript template with electron dependency added. It provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

This templates also offers a preconfigured debug that works in the 'main' and 'renderer' proceses at the same time.

## Getting started

1. Clone this Repo.
2. Use `npm install` to install all dependencies
3. Execute the `dev:electron` script to launch the app.

> **Note**:  
> You may want to update the version of the dependencies.

## Structure and overview

-   The **React** files are stored in the `src/ui` folder except the `index.html` that have to be in the root folder. The output files goes to the `dist-react` folder.
-   The **Electron** files are stored in the `src/electron` folder. The output files goes to the `dist-electron` folder.

This template is designed to make electron work with the transpiled files stored in the `dist-electron` and `dist-react` folders.

## Scripts and debug

**Nodemon** is used to watch for file changes. `nodemon.json` contains a basic configuration.

-   **dev:electron**: The mains script. Launch the Electron app and watch for file changes.
-   **dev:ui-only**: Launch the Vite server with the React project. Use this if you only want to work on UI side, but Electron queries will not work.
-   **watch**: Executes the nodemon watch service on all files located in the `src` folder. Every changes will make nodemon transpile all the 'src' folder.
-   **build**: Transpile the React and Electron TypeScript files to the JavaScript files in theire corresponding dist directories.
-   **lint**: Launch the EsLint check.
-   **preview**: Same as `dev:ui-only` but with transpiled files. This command is usefull to check how UI will look in production.
-   **dist:win**: Electron-builder script to create Windows distributables. Output files are stored in the `dist` folder.
-   **dist:mac**: Electron-builder script to create Mac distributables. Output files are stored in the `dist` folder.
-   **dist:linux**: Electron-builder script to create Linux distributables. Output files are stored in the `dist` folder.

Modify the electron-builder.json file to generate the output you want.

> **Note:**  
> Electron-builder recommends you to build the packages on the corresponding OS. What it means that you should run `dist:win` on Windows.

If you want to debug the app:

1. Add the breakpoints in your code.
2. Open the VSCode debug panel and select `Electron: All" in the `RUN AND DEBUG` selector. and press the play button or F5.

The App will automatically launch in debug mode with the Nodemon watch activated.
When you make changes to the files, Nodemon will generate the new files. You will need to `restart` (or press Ctrl + Shift + F5) the debugger to display the changes.

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

-   Configure the top-level `parserOptions` property like this:

```js
export default tseslint.config({
    languageOptions: {
        // other options...
        parserOptions: {
            project: ["./tsconfig.node.json", "./tsconfig.app.json"],
            tsconfigRootDir: import.meta.dirname
        }
    }
});
```

-   Replace `tseslint.configs.recommended` to `tseslint.configs.recommendedTypeChecked` or `tseslint.configs.strictTypeChecked`
-   Optionally add `...tseslint.configs.stylisticTypeChecked`
-   Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and update the config:

```js
// eslint.config.js
import react from "eslint-plugin-react";

export default tseslint.config({
    // Set the react version
    settings: { react: { version: "18.3" } },
    plugins: {
        // Add the react plugin
        react
    },
    rules: {
        // other rules...
        // Enable its recommended rules
        ...react.configs.recommended.rules,
        ...react.configs["jsx-runtime"].rules
    }
});
```
