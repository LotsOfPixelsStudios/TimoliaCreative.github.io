# Installation

### TL;DR

Create a project using the provided [Template](https://github.com/TimoliaCreative/TranClate-Template), add
the `~/.gradle/env-timoliacreative.local.gradle.kts` config to use tranclate.

## Template

Create a new project using the [Template](https://github.com/TimoliaCreative/TranClate-Template) on GitHub. Within this
template you can find the structure for a typical TranClate Project.

Within the Template you can also find Actions to build and release the project. When pushing to the default branch,
GitHub Actions will build the Addon and will make add a release with a `.mcworld` file in the release.

Note: he Template is build on JDK-17 and uses libraries only compatible with the JDK-17.

## Config

To access TranClate and the TranClate standard library you need to add a config for authentication in the `.gradle`
directory. The complete path is `~/.gradle/env-timoliacreative.local.gradle.kts` (while "~" is the home directory).

The file structure is as follows:

```kotlin
project.extra["maven_repo_user"] = "<user>"
project.extra["maven_repo_pw"] = "<token>"
project.extra["maven_repo_url"] = "<url>"
```

If you don't have an access file and want to use TranClate, write an e-mail
to [contact@timoliacreative.de](mailto:contact@timoliacreative.de) with regards for an access key for TranClate.

## Gradle

The whole project is build with gradle. To guarantee a working project ensure:

- use JDK-17 or higher
- use gradle 7.2 or higher
- use kotlin 1.6.20 or higher (already set within the `build.gradle.kts`)
- use the latest TranClate version, breaking changes are done gradually with deprecations (The Template will be kept up
  to date)