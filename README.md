# dxw's Scripts to Rule Them All

Template scripts to use in projects, based on
[GitHub's pattern](https://github.com/github/scripts-to-rule-them-all) with the
same name.

## Installation

For each language or stack, we have a set of scripts. To add them to a project,
copy the full contents of the most appropriate folder to the root of the project
and edit as needed. `base` is a good starting point if there's nothing more
appropriate.

## Contents

The template scripts for each language or stack assume the use of dxw's standard
tools.

### `script/bootstrap`

`script/bootstrap` should install all dependencies required to develop, build,
and run the application.

The script can assume that any macOS environment uses Homebrew for package
management and already has it installed. It can also assume that any
non-development environment (such as CI) will install system dependencies prior
to running the script.

### `script/setup`

`script/setup` should set the application up in its initial state. If this isn't
the first time working on a application, that means clearing any data or build
artefacts, to return the application to a pristine state.

This should run `script/bootstrap` as an early step.

### `script/update`

`script/update` should update the application to the latest configuration from
any earlier version. This should update any dependencies and run any database
migrations.

This should run `script/bootstrap` as an early step.

### `script/test`

`script/test` should run the full test suite, including any linters. Linting
tends to run faster than tests, so it's useful to put them first, so the suite
fails faster.

A useful pattern to support is having an optional argument, a file path or
pattern, for running a subset of the full suite.

This script should support being run in CI environments. If detection of the CI
environment is required, use the presence of a `CI` environment variable.

This should run `script/update` as an early step.

### `script/server`

If appropriate, `script/server` should start the application and any additional
processes needed to support it.

This should run `script/update` as an early step.

### `script/build`

If appropriate, `script/build` should create a production build of the
application.

A useful pattern to support is having an optional argument to specify the target
environment to build for.

This should run `script/update` as an early step.

### `script/console`

If appropriate, `script/console` should open a console for the application.

A useful pattern to support is having an optional argument to specify an
environment, to support connecting to other environments, like staging or
production. By default, it should connect to the local development environment.

This should also do any setup required to connect to the console for the given
environment.

### No `script/cibuild`

We choose not to use a single build script for CI, preferring instead to have
explicit steps in our CI configuration.
