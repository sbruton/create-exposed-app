# Developing

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [How do I setup the project for development?](#how-do-i-setup-the-project-for-development)
- [What's the development workflow?](#whats-the-development-workflow)
- [Why do my files automatically change?](#why-do-my-files-automatically-change)
- [I can't make a "Work in progress" commit because the build is broken](#i-cant-make-a-work-in-progress-commit-because-the-build-is-broken)
- [Why are the dev tools scripts so verbose?](#why-are-the-dev-tools-scripts-so-verbose)
- [Why are there so many config files?](#why-are-there-so-many-config-files)
- [Why isn't the build bundled or minified?](#why-isnt-the-build-bundled-or-minified)
- [Why does the Babel build script contain the `--source-maps` option?](#why-does-the-babel-build-script-contain-the---source-maps-option)
- [Why does the `format-eslint` script ignore errors?](#why-does-the-format-eslint-script-ignore-errors)
- [Why does the `start-src` script use `--require node_modules/dotenv/config`?](#why-does-the-start-src-script-use---require-node_modulesdotenvconfig)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## How do I setup the project for development?

1. If you don't have write access to this repo, [fork it](https://github.com/iamturns/create-exposed-app/fork)
1. Clone the repo
1. Install dependencies: `npm ci`
1. Ensure everything is working: `npm run validate`
1. Use VS Code? Run command `Extensions: Show Recommended Extensions` and install

## What's the development workflow?

1. Create a system-wide link for use in other directories: `npm link`
1. Start develop mode: `npm run dev`
1. For TDD fans: `npm run test--watch`
1. Write code
1. Create new temporary directory to test app population named `create-exposed-app-test-my-new-feature`
1. Run `npx create-exposed-app` in new directory

   Note: This should reference your local `create-exposed-app` copy, setup by previous linking command

1. Create a [pull request on GitHub](https://github.com/iamturns/create-exposed-app/pulls)
1. Remove the system-wide link: `npm unlink`
1. Remove the temporary test directory `create-exposed-app-test-my-new-feature`

## Why do my files automatically change?

See [ADR-005: Format Files](docs/adr/005-format-files.md) and [ADR-006: Format Files Programmatically](docs/adr/006-format-files-programmatically.md).

## I can't make a "Work in progress" commit because the build is broken

Include the `--no-verify` option during the commit:

```bash
git commit -m "WIP" --no-verify
```

## Why are the dev tools scripts so verbose?

See [ADR-002: Prefer Configurable Dev Tools](docs/adr/002-prefer-configurable-dev-tools.md).

## Why are there so many config files?

See [ADR-003: Prefer Multiple Config Files](docs/adr/003-prefer-multiple-config-files.md).

## Why isn't the build bundled or minified?

See [ADR-004: Minimally Transform Source Code During Build](docs/adr/004-minimally-transform-source-code-during-build.md).

## Why does the Babel build script contain the `--source-maps` option?

This option is available in the Babel config file (`sourceMaps: true`), but has diffrent behaviour. Only the command line supports the creation of `.map` files. See [https://github.com/babel/babel/issues/5261](https://github.com/babel/babel/issues/5261).

## Why does the `format-eslint` script ignore errors?

Linting errors should not be reported when formatting, that it was the `lint` command is for.

Errors are ignored by appending the following: `>/dev/null 2>&1 || true`.

## Why does the `start-src` script use `--require node_modules/dotenv/config`?

The [recommended setup](https://github.com/motdotla/dotenv#preload) advises preloading with `--require dotenv/config`. However due to a [known problem in Babel](https://github.com/babel/babel/issues/8229), this must be prefixed with `node_modules`.
