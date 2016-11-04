# tslint-cgalvarez

## Purpose

This project includes a variety of tslint rules I use for my projects.

I find useful the following sets of rules:

* [buzinas/tslint-eslint-rules](https://github.com/buzinas/tslint-eslint-rules)
* [Microsoft/tslint-microsoft-contrib](https://github.com/Microsoft/tslint-microsoft-contrib)
* [vrsource/vrsource-tslint-rules](https://github.com/vrsource/vrsource-tslint-rules)

but I want to avoid the following issues:

* having to manually include them as devDependencies in each one of my TypeScript projects.
* having to manually include their set of rules/directories in each one of my TypeScript project's `tsconfig.json`.
* dealing with the [tslint errors](https://github.com/palantir/tslint/issues/1522) of the atom package [`linter-tslint`](https://github.com/AtomLinter/linter-eslint) due to rules that require the still unsupported flag `--type-check`.

so I've come publishing this package that extends the `tslint:latest` set of rules and implements all the rules of the previously listed set of rules in two separate files that you should extend in your `tsconfig.json`.

## Usage

Add it as git devDependency (not published to the NPM registry yet, sorry) as follows:

```json
{
    "tslint-cgalvarez-rules": "https://github.com/cgalvarez/tslint-cgalvarez-rules/tarball/master",
}
```

Configure tslint to use the `tslint-cgalvarez-rules` rules in your `tslint.json` as follows:

```json
{
   "extends": "tslint-cgalvarez-rules/tslint.json",
   "rules": {
     ...
   }
}
```

You can configure any rule if you find in need to do so through the `rules` key of your `tslint.json`. Check the previously extended file if you need help with any rule (the help URL to each rules set is listed at the very beginning of each section).

There are two different files you can extend:

* `tslint-cgalvarez-rules/tslint.json`: use it when executing tslint from command line or CI.
* `tslint-cgalvarez-rules/tslint-ide.json`: use it when using atom.

Since you cannot provide a custom path to your `tslint.json` when using the atom package `linter-tslint`, I recommend extending `tslint-cgalvarez-rules/tslint-ide.json` in your `tslint.json`, and creating a separate `tslint-cl.json` which extends `tslint-cgalvarez-rules/tslint.json` and can be provided in the command line like `tslint --config tslint-cl.json --type-check ...`.
