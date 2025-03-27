# Example of JF CLI and Artifactory Gradle Plugin

In order to be able to publish to Snapshot and Release repositories individually, it appears to be necessary to use the Artifactory Gradle Plugin.  

The key parts to the config include:
* run `jf gradlec`, specifying dependency resolution repository and any publishing repositories (although these will be overridden in the Artifactory Gradle Plugin's `artifactory` block.)
* Selecting to use the Gradle Artifactory Plugin that's applied in the build script:
```bash
jf gradle-config
...
...
Is the Gradle Artifactory Plugin already applied in the build script? (y/n) [n]? y <-----------
```
* Using the `maven-publish` plugin
* Configuring the `artifactory` block in the `build.gradle` spec
* Executing the Gradle task `artifactoryPublish`

```bash
jf gradle clean build artifactoryPublish --build-name foo --build-number 1
jf rt bp foo 1
```

## Not Yet Tested
1. Precedence for Dependency Resolution if both are configued in JF Gradle config (`.jfrog/gradle.yaml`) and in the `repositories` block in `build.gradle`. The test would be to set two different dependency repositories, and select one for use in the `jf gradle-config` command, and another one in the `repositories` block and see which one gets the dependencies cached.
2. A means to set different repositories for Snapshot and Release _dependencies_.  It's not clear if this is supported in Gradle altogether.  

## Advantage of using the JF CLI Gradle integration
The JF CLI connection config is used for the Gradle build, as well as Build Info recording and publishing.  It is also possible to configure the build info details directly in the Artifactory Plugin `artifactory` block as well.

The credentials use is particularly convenient if you are using the OIDC authentication as the JF CLI will use the OIDC-sourced token for authentication.  If you don't use the JF CLI, you'll have to pass static credentials in as Env Vars or Gradle Properties. 