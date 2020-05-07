<!-- omit in toc -->
# Git Usage


- [1. Writing commits](#1-writing-commits)
  - [1.1 Types](#11-types)
  - [1.2 Scope (optional)](#12-scope-optional)
  - [1.3 Subject](#13-subject)
  - [1.4 Body (optional)](#14-body-optional)
- [2. Examples](#2-examples)
- [3. Specification](#3-specification)
- [3. Additional Reading](#3-additional-reading)


## 1. Writing commits

Commits should be informative and specific, targetting specific files with details on what they're
doing.

On projects with our full linting setup, there will be a commit linter which will prevent you from
being able to make commits unless it follows specific conventions. It can't enforce everything
below, but

```txt
<type>([optional scope]): <subject>

[optional body]

[optional footer]
```

Examples can be found below.

### 1.1 Types

- **feat**: A new feature (this correlates with MINOR in semantic versioning)
- **fix**: A bug fix (this correlates with PATCH in semantic versioning).
- **docs**: Documentation only changes
- **style**: Changes that dont affect the meaning of the code (white-space formatting, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing or correcting existing tests
- **chore**: Changes to the build process or auxiliary tools and libraries (exampl\* scopes: gulp,
  broccoli, npm)
- **ci**: Changes to our CI configuration files and scripts (example scopes: Travis, Circle,
  BrowserStack, SauceLabs)

### 1.2 Scope (optional)

- The module/scope that your commit targets.

### 1.3 Subject

- use imperative, present tense: "change", not "changed" or "changes"
- don't capitalize first letter
- no period at the end

### 1.4 Body (optional)

Can be used to describe the commit in more detail. To add a body, hit return twice while typing your
commit in, like this

```sh
git commit -m "feat: example commit (hit return twice)

BREAKING CHANGE: Talk about what the breaking change is here." (return again to close out your commit)
```

The body can have some nifty integrations with other tools to make things easier:

- Github can automatically close related issues if you include `closes` in the body. For example,
  writing `closes: #123` will automagically close issue #123 in Github. The colon is optional, but
  the `#` is not. For multiple issues, just write `closes #123, closes #456`. The separations aren't
  important, just the presence of `closes`.

- `BREAKING CHANGE:` indicates that you're introducing a breaking API change (i.e., a MAJOR semvar
  update). `BREAKING CHANGE:` must be followed with an explanation

## 2. Examples

Commit message with description and breaking change in body

```txt
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files.

Closes DIC-34
```

Commit message with no body

```txt
docs: correct spelling of CHANGELOG
```

Commit message with scope

```txt
feat(lang): add polish language
```

Commit message for a fix using an (optional) issue number

```txt
fix: minor typos in code

see the issue for details on the typos fixed

Closes #12
```

## 3. Specification

Taken from [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.3/).

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”,
“RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in
[RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

1. Commits MUST be prefixed with a type, which consists of a noun, feat, fix, etc., followed by a
   colon and a space.
2. The type feat MUST be used when a commit adds a new feature to your application or library.
3. The type fix MUST be used when a commit represents a bug fix for your application.
4. An optional scope MAY be provided after a type. A scope is a phrase describing a section of the
   codebase enclosed in parenthesis, e.g., fix(parser):
5. A description MUST immediately follow the type/scope prefix. The description is a short
   description of the code changes, e.g., fix: array parsing issue when multiple spaces were
   contained in string.
6. A longer commit body MAY be provided after the short description, providing additional contextual
   information about the code changes. The body MUST begin one blank line after the description.
7. A footer MAY be provided one blank line after the body. The footer SHOULD contain additional
   issue references about the code changes (such as the issues it fixes, e.g.,Fixes #13).
8. Breaking changes MUST be indicated at the very beginning of the footer or body section of a
   commit. A breaking change MUST consist of the uppercase text BREAKING CHANGE, followed by a colon
   and a space.
9. A description MUST be provided after the BREAKING CHANGE:, describing what has changed about the
   API, e.g., BREAKING CHANGE: environment variables now take precedence over config files.
10. The footer MUST only contain BREAKING CHANGE, external links, issue references, and other
   meta-information.
11. Types other than feat and fix MAY be used in your commit messages.

## 3. Additional Reading

- [Commit lint rules](https://github.com/marionebl/commitlint/tree/master/%40commitlint/config-conventional)
- [Codfish git reference](https://gist.github.com/codfish/87ddae4b7fdbb3decf07)
- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.3/)
