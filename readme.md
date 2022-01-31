![](https://github.com/js-soft/better-lerna-audit/workflows/CI/badge.svg)

# Lerna Audit

Micro util to run npm audit for lerna packages (with autofix).

## How to use

### Install

In the root of your lerna monorepo run:

`npm i better-lerna-audit -D`

or

`yarn add better-lerna-audit -D`

### Use

In the root of your lerna monorepo run:

`npx better-lerna-audit [OPTIONS]`

Or add a script to your `package.json` in root:

```jsonc
{
  "scripts": {
    "audit": "better-lerna-audit"
  }
}
```

#### Options

| Parameter | Default | Description                                          |
| --------- | ------- | ---------------------------------------------------- |
| `--fix`   | false   | (optional) Fix the found vulnerabilities, just audit |

## Why

Lerna works in a way that it manages "internal" dependencies within your monorepo by managing all relevant `npm link` commands for you in local development. So you can keep the dependencies to other packages in the monorepo in your package.json while linking the latest versions during development. The downside is that all commands that depend on the dependencies defined in `package.json`s will fail because "internal" packages are just linked and not yet published. One of this commands is `npm audit` because it tires to analyse the dependency tree. `better-lerna-audit` mimics the behavior of lerna - removing internal packages from package.json, run the command, restore package.json - to run a `npm fix` in every lerna managed package.
