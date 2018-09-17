<!-- markdownlint-disable MD012 MD014 -->

# TeamCity

## Build project as code



![Chef Giphy](https://media.giphy.com/media/xznyPebL28X5u/giphy.gif)


## Infrastructure as Code

> Defining computing and network infrastructure through source code that can then be treated just like any software system

[Martin Fowler](https://martinfowler.com/bliki/InfrastructureAsCode.html)


### Benefits

- Can be kept in  version control
- Allows reproducible builds and testing
- Reduced mean time to recovery when disaster strikes
  - Roll back to latest working configuration


### Example Travis CI

- Keep build configuration alongside the code in the same VCS
- Pick an external form for the build configuration that is
  - plain text and
  - is human readable

&rightarrow; Changes can be tracked and diffed much like the changes to any other part of the code


- CI build is represented as [YAML](https://en.wikipedia.org/wiki/YAML) file.
  - Add `.travis.yml` file to the repository
- Ruby example

```yml
language: ruby
rvm:
 - 2.2
 - jruby
```

- Java example

```yml
language: java
jdk:
  - oraclejdk8
  - oraclejdk9
  - openjdk8
```



## TeamCity


### Current situation

- Build project can be configured via Web UI
- "Build project as code" disabled per default
  - JetBrains used "Versioned Settings" as feature name


### Versioned settings

- Allows the two-way synchronization of the project settings with the VCS
- Settings can be stored in XML format and in [Kotlin](https://kotlinlang.org/) language
- Settings are stored in the `.teamcity` folder in the root of the repository


When two-way settings synchronization is enabled  

- Each administrative change made to the project settings in the TeamCity Web UI is committed to VCS
- Committer is the TeamCity user
- If a settings change is committed to VCS, the TeamCity server will
  - detect the modifications and
  - apply them to the project on the fly


- Before applying the newly checked-in settings, certain constraints are applied
- If the constraints are not met, current settings are left intact and an error is shown in the UI.


- Enabling/ disabling versioned settings is a specific permission
- Per default not attached to Project developers (plus) role



Example code

```kotlin
create(DslContext.projectId, BuildType({
    id("Verify")
    name = "Test"
    vcs { root(DslContext.settingsRoot) }
    steps {
        gradle {
            name = "Build"
            tasks = "clean test"
        }
        ideaInspections {
            pathToProject = "build.gradle"
            jvmArgs = "-Xmx512m -XX:ReservedCodeCacheSize=240m"
            targetJdkHome = "%env.JDK_18%"
        }
    }
    triggers { vcs { } }
}))
```


## Questions?



## Further information

- [Infrastructure as Code](https://martinfowler.com/bliki/InfrastructureAsCode.html)
- [Travis CI](https://travis-ci.org/)
- [Storing Project Settings in Version Control](https://confluence.jetbrains.com/display/TCD18/Storing+Project+Settings+in+Version+Control)