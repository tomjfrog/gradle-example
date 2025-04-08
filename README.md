# Example of JF CLI and Artifactory Gradle Plugin

In order to be able to publish to Snapshot and Release repositories individually, it appears to be necessary to use the Artifactory Gradle Plugin.  

This is a basic working example that requires:
1. Env Vars for
   2. Username
   3. Password
   4. Build Number.  Since this likely will be run in Github Actions, set the Env Var for the run step to `${{ github.run_number }}`

Execute:
```bash
gradle clean build artifactoryPublish
```