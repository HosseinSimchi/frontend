### `scripts`

1- Remove cache.

- "rm-cache": "sudo rm -rf .angular/",

2- If you want to run the tests and Chrome does not open automatically, and also the user password is taken as sudo before running the tests.

- "Test": "sudo -v && ng test --browsers ChromeHeadlessNoSandbox",

3- If you want to have the coverage test.

- "Coverage": "sudo -v && ng test --browsers ChromeHeadlessNoSandbox --no-watch --code-coverage",

### create `karma.conf.js`

```javascript
// Karma configuration file, see link for more information
// https://karma-runner.github.io/1.0/config/configuration-file.html
const webpack = require("webpack");

module.exports = function (config) {
  config.set({
    basePath: "",
    frameworks: ["jasmine", "@angular-devkit/build-angular"],
    plugins: [
      require("karma-jasmine"),
      require("karma-chrome-launcher"),
      require("karma-jasmine-html-reporter"),
      require("karma-coverage"),
      require("karma-junit-reporter"), // اضافه کردن پلاگین karma-junit-reporter
      require("@angular-devkit/build-angular/plugins/karma"),
    ],
    client: {
      jasmine: {
        // you can add configuration options for Jasmine here
        // the possible options are listed at https://jasmine.github.io/api/edge/Configuration.html
        // for example, you can disable the random execution with `random: false`
        // or set a specific seed with `seed: 4321`
      },
      clearContext: false, // leave Jasmine Spec Runner output visible in browser
    },
    jasmineHtmlReporter: {
      suppressAll: true, // removes the duplicated traces
    },
    coverageReporter: {
      dir: require("path").join(__dirname, "./coverage/mindharvest"),
      subdir: ".",
      reporters: [
        { type: "html" },
        { type: "text-summary" },
        { type: "cobertura", subdir: ".", file: "cobertura-coverage.xml" }, // اضافه کردن گزارش cobertura
      ],
    },
    junitReporter: {
      outputDir: "coverage", // مسیر خروجی فایل JUnit
      outputFile: "junit-report.xml", // نام فایل گزارش
      useBrowserName: false, // عدم استفاده از نام مرورگر در نام فایل
    },
    reporters: ["progress", "kjhtml", "junit"], // افزودن junit به reporters
    port: 9876,
    colors: true,
    logLevel: config.LOG_INFO,
    autoWatch: true,
    browsers: ["Chrome"],
    customLaunchers: {
      ChromeHeadlessNoSandbox: {
        base: "ChromeHeadless",
        flags: ["--no-sandbox"],
      },
    },
    singleRun: false,
    restartOnFileChange: true,

    // Webpack configuration to polyfill global
    webpack: {
      plugins: [
        new webpack.ProvidePlugin({
          global: require.resolve("globalthis/polyfill"), // Polyfill for global object
        }),
      ],
    },
  });
};
```

### `tsconfig.spec.json`

```javascript
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": ["jasmine"]
  },
  "include": ["src/**/*.spec.ts", "src/**/*.d.ts"],
}

```

### `angular.json`

_inside the "architect" part_

```javascript
"test": {
          "builder": "@angular-devkit/build-angular:karma",
          "options": {
            "polyfills": ["zone.js", "zone.js/testing"],
            "tsConfig": "tsconfig.spec.json",
            "assets": [
              {
                "glob": "**/*",
                "input": "public"
              }
            ],
            "styles": [
              "@angular/material/prebuilt-themes/rose-red.css",
              "src/styles.css"
            ],
            "scripts": []
          }
        }
```
