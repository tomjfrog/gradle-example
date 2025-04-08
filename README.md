# Example of JF CLI and Artifactory Gradle Plugin

In order to be able to publish to Snapshot and Release repositories individually, it appears to be necessary to use the Artifactory Gradle Plugin.  

This is a basic working example that requires:
## Environment Variables for:
1. Username
1. Password
1. Build Number.  Since this likely will be run in Github Actions, set the Env Var for the run step to
`${{ github.run_number }}`

Execute:
```bash
gradle clean build artifactoryPublish
```