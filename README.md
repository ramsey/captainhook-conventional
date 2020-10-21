<h1 align="center">ramsey/conventional-commits</h1>

<p align="center">
    <strong>A PHP library for creating and validating commit messages.</strong>
</p>

<p align="center">
    <a href="https://github.com/ramsey/conventional-commits"><img src="http://img.shields.io/badge/source-ramsey/conventional--commits-blue.svg?style=flat-square" alt="Source Code"></a>
    <a href="https://packagist.org/packages/ramsey/conventional-commits"><img src="https://img.shields.io/packagist/v/ramsey/conventional-commits.svg?style=flat-square&label=release" alt="Download Package"></a>
    <a href="https://php.net"><img src="https://img.shields.io/packagist/php-v/ramsey/conventional-commits.svg?style=flat-square&colorB=%238892BF" alt="PHP Programming Language"></a>
    <a href="https://github.com/ramsey/conventional-commits/actions?query=workflow%3ACI"><img src="https://img.shields.io/github/workflow/status/ramsey/conventional-commits/CI?logo=github&style=flat-square" alt="Build Status"></a>
    <a href="https://codecov.io/gh/ramsey/conventional-commits"><img src="https://img.shields.io/codecov/c/gh/ramsey/conventional-commits?label=codecov&logo=codecov&style=flat-square" alt="Codecov Code Coverage"></a>
    <a href="https://shepherd.dev/github/ramsey/conventional-commits"><img src="https://img.shields.io/endpoint?style=flat-square&url=https%3A%2F%2Fshepherd.dev%2Fgithub%2Framsey%2Fconventional-commits%2Fcoverage" alt="Psalm Type Coverage"></a>
    <a href="https://github.com/ramsey/conventional-commits/blob/master/LICENSE"><img src="https://img.shields.io/packagist/l/ramsey/conventional-commits.svg?style=flat-square&colorB=darkcyan" alt="Read License"></a>
    <a href="https://packagist.org/packages/ramsey/conventional-commits/stats"><img src="https://img.shields.io/packagist/dt/ramsey/conventional-commits.svg?style=flat-square&colorB=darkmagenta" alt="Package downloads on Packagist"></a>
    <a href="https://phpc.chat/channel/ramsey"><img src="https://img.shields.io/badge/phpc.chat-%23ramsey-darkslateblue?style=flat-square" alt="Chat with the maintainers"></a>
</p>

## About

ramsey/conventional-commits is a PHP library for creating and validating commit
messages according to the [Conventional Commits specification][]. It also
includes a [CaptainHook][] plugin!

This project adheres to a [code of conduct](CODE_OF_CONDUCT.md).
By participating in this project and its community, you are expected to
uphold this code.

## Installation

Install this package as a development dependency using
[Composer](https://getcomposer.org).

``` bash
composer require --dev ramsey/conventional-commits
```

## Usage

To use the `conventional-commits` console command to help you prepare commit
messages according to Conventional Commits, enter the following in your console:

``` bash
./vendor/bin/conventional-commits prepare
```

To see all the features of the console command, enter:

``` bash
./vendor/bin/conventional-commits
```

### Validating Commit Messages

To use the CaptainHook plugin to validate commit messages according to the
Conventional Commits specification, add the following to the `commit-msg`
property in your `captainhook.json` file:

``` json
{
    "commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\ValidateConventionalCommit"
            }
        ]
    }
}
```

### Preparing Commit Messages

You can set up this library to prompt you to prepare commit messages when you
use `git commit`!

To use the CaptainHook plugin to prepare commit messages according to the
Conventional Commits specification, add the following to the `prepare-commit-msg`
property in your `captainhook.json` file:

``` json
{
    "prepare-commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\PrepareConventionalCommit"
            }
        ]
    }
}
```

### Configuration

Configuring ramsey/conventional-commits offers control over a few more aspects
of commit messages, such as letter case (i.e. lower, upper), allowed types and
scopes, required footers, and more.

We look for configuration in one of two places:

* `composer.json`
* `captainhook.json`

> ⚠️ **Please note:** if your `composer.json` file is not in the same location as
> the `vendor/` directory, we might have trouble locating it. Feel free to open
> an issue, and we'll work with you to see if we can find a solution.

#### Configuration Properties

Configuration for ramsey/conventional-commits consists of the following
properties:

| Property             | Description |
| -------------------- | ----------- |
| `typeCase`           | The letter case to require for the type. By default, any letter case is acceptable.
| `types`              | An array of accepted types (in addition to "feat" and "fix"). By default, any type is acceptable.
| `scopeCase`          | The letter case to require for the scope. By default, any letter case is acceptable.
| `scopeRequired`      | Whether a scope is required. By default, scope is not required.
| `scopes`             | An array of accepted scopes. By default, any scope is acceptable.
| `descriptionCase`    | The letter case to require for the description. By default, any letter case is acceptable.
| `descriptionEndMark` | A character to require at the end of the description. By default, any character is allowed. Use an empty string to indicate a punctuation character is not allowed at the end of the description.
| `bodyRequired`       | Whether a body is required. By default, a body is not required.
| `bodyWrapWidth`      | An integer indicating the character width to auto-wrap the body of the commit message. By default, the commit body does not auto-wrap.
| `requiredFooters`    | An array of footers that must be provided. By default, footers are not required.

When specifying configuration, if you wish to use the default behavior for a
property, it is not necessary to list the property in your configuration.

Recognized letter cases are:

| Identifier | Name          | Example |
| ---------- | ------------- | ------- |
| `ada`      | Ada case      | `The_Quick_Brown_Fox`
| `camel`    | Camel case    | `theQuickBrownFox`
| `cobol`    | COBOL case    | `THE-QUICK-BROWN-FOX`
| `dot`      | Dot notation  | `the.quick.brown.fox`
| `kebab`    | Kebab case    | `the-quick-brown-fox`
| `lower`    | Lower case    | `the quick brown fox`
| `macro`    | Macro case    | `THE_QUICK_BROWN_FOX`
| `pascal`   | Pascal case   | `TheQuickBrownFox`
| `sentence` | Sentence case | `The quick brown fox`
| `snake`    | Snake case    | `the_quick_brown_fox`
| `title`    | Title case    | `The Quick Brown Fox`
| `train`    | Train case    | `The-Quick-Brown-Fox`
| `upper`    | Upper case    | `THE QUICK BROWN FOX`

#### Configuration in composer.json

If you choose to put your configuration in `composer.json`, place it within the
`extra` property, namespaced under `ramsey/conventional-commits`, like this:

``` json
{
    "extra": {
        "ramsey/conventional-commits": {
            "config": {
                "typeCase": null,
                "types": [],
                "scopeCase": null,
                "scopeRequired": false,
                "scopes": [],
                "descriptionCase": null,
                "descriptionEndMark": null,
                "bodyRequired": false,
                "bodyWrapWidth": null,
                "requiredFooters": []
            }
        }
    }
}
```

> 📝 The properties in this example represent the default values.

#### Configuration in captainhook.json

If you choose to put your configuration in `captainhook.json`, you must provide
it for *each action* you configure, like this:

``` json
{
    "commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\ValidateConventionalCommit",
                "options": {
                    "config": {
                        "typeCase": null,
                        "types": [],
                        "scopeCase": null,
                        "scopeRequired": false,
                        "scopes": [],
                        "descriptionCase": null,
                        "descriptionEndMark": null,
                        "bodyRequired": false,
                        "bodyWrapWidth": null,
                        "requiredFooters": []
                    }
                }
            }
        ]
    },
    "prepare-commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\PrepareConventionalCommit",
                "options": {
                    "config": {
                        "typeCase": null,
                        "types": [],
                        "scopeCase": null,
                        "scopeRequired": false,
                        "scopes": [],
                        "descriptionCase": null,
                        "descriptionEndMark": null,
                        "bodyRequired": false,
                        "bodyWrapWidth": null,
                        "requiredFooters": []
                    }
                }
            }
        ]
    }
}
```

However, if you provide your configuration in `composer.json`, it is not
necessary to also provide it in `captainhook.json`.

> 🚨 If using the Git commit hook functionality of Captain Hook, any
> configuration provided in `captainhook.json` will override configuration
> in `composer.json`.
>
> ⚠️ When using the standalone command (i.e. `./vendor/bin/conventional-commits`),
> only configuration in `composer.json` will apply, unless providing the
> `--config` option.

#### Configuration in a Separate File

You may also store your configuration in a separate file. For example, you may
store it in `conventional-commits.json`, like this:

``` json
{
    "typeCase": "kebab",
    "types": [
        "ci",
        "deps",
        "docs",
        "refactor",
        "style",
        "test"
    ],
    "scopeCase": "kebab",
    "scopeRequired": false,
    "scopes": [],
    "descriptionCase": "lower",
    "descriptionEndMark": "",
    "bodyRequired": true,
    "bodyWrapWidth": 72,
    "requiredFooters": ["Signed-off-by"]
}
```

When stored in a separate file, we won't know where to look for your
configuration, unless you tell us, so you must still provide a small amount of
configuration in either `composer.json` or `captainhook.json`, so we can find
it.

Here's what this looks like in `composer.json`:

``` json
{
    "extra": {
        "ramsey/conventional-commits": {
            "configFile": "./conventional-commits.json"
        }
    }
}
```

And here's what this looks like in `captainhook.json`:

``` json
{
    "commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\ValidateConventionalCommit",
                "options": {
                    "configFile": "./conventional-commits.json"
                }
            }
        ]
    },
    "prepare-commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\PrepareConventionalCommit",
                "options": {
                    "configFile": "./conventional-commits.json"
                }
            }
        ]
    }
}
```

## Contributing

Contributions are welcome! Before contributing to this project, familiarize
yourself with [CONTRIBUTING.md](CONTRIBUTING.md).

To develop this project, you will need [PHP](https://www.php.net) 7.4 or greater
and [Composer](https://getcomposer.org).

After cloning this repository locally, execute the following commands:

``` bash
cd /path/to/conventional-commits
composer install
```

Now, you are ready to develop!

### Tooling

This project uses [CaptainHook](https://github.com/CaptainHookPhp/captainhook)
to validate all staged changes prior to commit.

#### Composer Commands

To see all the commands available in the project `dev` namespace for
Composer, type:

``` bash
composer list dev
```

#### Coding Standards

This project follows a superset of [PSR-12](https://www.php-fig.org/psr/psr-12/)
coding standards, enforced by [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer).
The project PHP_CodeSniffer configuration may be found in `phpcs.xml.dist`.

CaptainHook will run PHP_CodeSniffer before committing. It will attempt to fix
any errors it can, and it will reject the commit if there are any un-fixable
issues. Many issues can be fixed automatically and will be done so pre-commit.

You may lint the entire codebase using PHP_CodeSniffer with the following
commands:

``` bash
# Lint
composer dev:lint

# Lint and autofix
composer dev:lint:fix
```

#### Static Analysis

This project uses a combination of [PHPStan](https://github.com/phpstan/phpstan)
and [Psalm](https://github.com/vimeo/psalm) to provide static analysis of PHP
code. Configurations for these are in `phpstan.neon.dist` and `psalm.xml`,
respectively.

CaptainHook will run PHPStan and Psalm before committing. The pre-commit hook
does not attempt to fix any static analysis errors. Instead, the commit will
fail, and you must fix the errors manually.

You may run static analysis manually across the whole codebase with the
following command:

``` bash
# Static analysis
composer dev:analyze
```

#### Project Structure

This project uses [pds/skeleton](https://github.com/php-pds/skeleton) as its
base folder structure and layout.

## Copyright and License

The ramsey/conventional-commits library is copyright © [Ben Ramsey](https://benramsey.com)
and licensed for use under the terms of the MIT License (MIT). Please see
[LICENSE](LICENSE) for more information.


[Conventional Commits specification]: https://www.conventionalcommits.org/en/v1.0.0/
[CaptainHook]: https://github.com/captainhookphp/captainhook
