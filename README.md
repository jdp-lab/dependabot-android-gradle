# dependabot-android-gradle

A Proof of Concept repo to test how [Dependabot](https://github.com/dependabot) can handle the dependencies from
https://maven.google.com

## Problem

We wanted to use Dependabot on an Android Gradle project. The problem is that Dependabot is only
checking https://repo.maven.apache.org for version updates with the [default configuration][dependabot-default-config].
However on an Android project needs a lots of dependencies which are provided by Google.

## Idea

Configure dependabot to be able to scan for dependencies in [https://maven.goolge.com](https://maven.goolge.com).

## Result

Dependabot will check for updates if a [maven registry][dependabot-registries] is set up
in [dependabot.yml][dependabot-google-config]:

```yaml
version: 2
registries:
  maven-google:
    type: maven-repository
    url: https://maven.google.com
    username: ""
    password: ""
updates:
  - package-ecosystem: "gradle"
    directory: "/"
    registries:
      - maven-google
    schedule:
      interval: "daily"
    open-pull-requests-limit: 10
```

[dependabot-default-config]: https://github.com/apter-tech/dependabot-android-gradle/commit/e200e9284fc7205e8e21c4bb36feefe414d5bd27

[dependabot-google-config]: https://github.com/apter-tech/dependabot-android-gradle/commit/9d8cc6f8152b494d761f296245859faf25a7a5ed

[dependabot-registries]: https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#registries