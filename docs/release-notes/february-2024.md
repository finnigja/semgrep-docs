---
slug: february-2024
hide_title: true
description: >-
    Release notes include the changes, fixes, and additions in specific versions of Semgrep.
toc_max_heading_level: 3
title: February 2024
tags:
  - Release notes
---

# Semgrep release notes for February 2024

## 🔧 OSS Engine

* The following versions of the OSS Engine were released in February 2024:
  * [<i class="fas fa-external-link fa-xs"></i>1.59.1](https://github.com/semgrep/semgrep/releases/tag/v1.59.1)
  * [<i class="fas fa-external-link fa-xs"></i>1.60.0](https://github.com/semgrep/semgrep/releases/tag/v1.60.0)
  * [<i class="fas fa-external-link fa-xs"></i>1.60.1](https://github.com/semgrep/semgrep/releases/tag/v1.60.1)
  * [<i class="fas fa-external-link fa-xs"></i>1.61.1](https://github.com/semgrep/semgrep/releases/tag/v1.61.1)
  * [<i class="fas fa-external-link fa-xs"></i>1.62.0](https://github.com/semgrep/semgrep/releases/tag/v1.62.0)
  * [<i class="fas fa-external-link fa-xs"></i>1.63.0](https://github.com/semgrep/semgrep/releases/tag/v1.63.0)

## 🌐 Cloud Platform

### Added

- API: Added a `rule` object under `findings` with the following fields: 
    - `name`
    - `message`
    - `confidence`
    - `category`
    - `subcategories`
    - `technologies`
    - `vulnerability_classes`
    - `cwe_names`
    - `owasp_names` <!-- 12868 --> 


### Changed

### Fixed

- Fixed a bug where the navigation sidebar covered mobile screens and could not be collapsed. <!-- 12876 -->

## 💻 Code

### Added

* Added new rules for Elixir and the Phoenix framework, covering various security and correctness issues. These are available in the `p/elixir`
  ruleset. <!-- Do we need to mention that this is for Pro users only? -->
* Added support for Python, with a focus on the Flask ecosystem, to the Semgrep
  Pro Engine.
* Added ability to collapse and turn off patterns in a rule.
* Added the ability to distinguish between which rules are available to Semgrep
  Pro Engine users and which ones are available to Semgrep OSS users.
* Added support for nested record patterns on the left-hand side of an
  assignment.
* `metavariable-regex` can now match on metavariables of interpolated strings
  that use variables with known values.
* Added support for parsing Swift Package Manager manifest files and lock files.
* **Taint analysis**:
  * Added support for Python constructors
  * Added support for index sensitivity. Semgrep tracks taint on individual
    indexes of a data structure when these are constant values, either integers
    or strings, and the code uses the built-in syntax for array indexing.
  * Added `exact: false` so you can specify that anything inside a code
    region is a sink.
  * When `exact: true` and `taint_assume_safe_functions: true`, Semgrep now
    considers that, if the specified formula isn't a `patterns` with a
    `focus-metavariable`, it must look for taint in the function call's arguments.

### Changed

* Improved error handling during inter-file analysis so Semgrep Code doesn't crash.
* **CLI**: If there are multiple errors resulting from the user running Pro
  rules without a paid subscription, the CLI groups all errors and reports a
  single warning.
* The project name for repositories scanned locally is `local_scan/<repo_name>`
  instead of `<repo_name>`.
* The **View Results** URL displayed for findings now includes the repository
  and branch names.

### Fixed

* Fixed issues with trailing newline parsing in `pyproject.toml` and
  `poetry.lock` files.
* Fixed an issue with incorrect autofix application where multiple fixes were
  applied to the same line.
* Fixed issue where tokens for type parameter brackets weren't stored correctly.
  They're now stored in the generic AST, allowing Semgrep to autofix
  these constructs correctly.
* Fixed an issue where Semgrep doesn't support multiple labels for taint
  traces. Now, Semgrep looks at the `requires` of the sink, and if it has the
  shape `A and ...`, it picks `A` as the preferred label and reports the
  trace.
* Fixed issue where taint signatures don't capture changes to parameter fields.
* Scan summary links printed after users run `semgrep ci` now reflect a
  custom `SEMGREP_APP_URL` if set.

## ⛓️ Supply Chain

### Added

* Added the ability to filter for dependencies that Semgrep has commented on.
  <!-- https://github.com/semgrep/semgrep-app/pull/12898 -->
* Added manual review advice to GitHub PR comments. Certain Semgrep Supply Chain (SSC) findings require **manual review** to verify if the finding is reachable or not. GitHub PR comments now include this advice to help you ascertain if the finding is reachable or not. <!-- 12907 -->

## 🤖 Assistant (beta)

### Added

- Added weekly emails summarizing Semgrep tasks, highlighting top priority items. <!-- Private beta - not sure if we should include this --> 

### Changed

### Fixed

## 🔐 Secrets (beta)

### Added

- Added the following new rules:
  - Detection rules for Azure and AWS
  - Semantic secrets rules for Python, JavaScript, and TypeScript
  - Semantic rules for hard-coded credentials in bash for `curl` commands
- Added non-validator regex detection for databases, including MongoDB,
  Microsoft SQL Server, MySQL, Postgres, and Redis
- Added secrets rule management, which is accessible in Semgrep Cloud Platform
  by going to **Rules** > **Policies** > **Secrets**. This allows you to:
  - See all available rules
  - Set valid finding modes for the rules
  - Set invalid and error validation state modes across multiple rules

### Fixed

- Fixed an issue where the **Analysis method** filter in Semgrep Cloud Platform
  wasn't filtering correctly.

## 📝 Documentation and knowledge base

### Added

### Changed

### Fixed
