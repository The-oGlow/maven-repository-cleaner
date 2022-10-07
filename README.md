[![Latest Release](https://img.shields.io/github/v/release/The-oGlow/maven-repository-cleaner?sort=semver&logo=github&style=plastic)](https://github.com/The-oGlow/maven-repository-cleaner/releases)
[![Software License](https://img.shields.io/badge/license-license-brightgreen?logo=github&style=plastic)](./LICENSE)

# What is this tool?

The Maven repository cleaner (bash script), which keeps only the latest versions of artifacts.

**This is a fork from [alitokmen/maven-repository-cleaner](https://github.com/alitokmen/maven-repository-cleaner)**.

# How does this tool work?

The bash `maven-repository-cleaner.sh` script

* verifies if the chosen directory is the root of the maven repository
* has the function, `cleanDirectory`, which is a recursive function looping through the `~/.m2/repository/` and does the following:
    * When the subdirectory is not a version number, it digs into that subdirectory for analysis
    * When a directory has subdirectories which appear to be version numbers, it only deletes all lower versions
* shows the used amount of diskspace before and after the clean up

In practice, if you have a hierarchy such as:

* `artifact-group`
    * `artifact-name`
        * `1.8`
        * `1.10`
        * `1.2`

the `maven-repository-cleaner.sh` script will:

1. Navigate to `artifact-group`
1. In `artifact-group`, navigate to `artifact-name`
1. In `artifact-name`, delete the subfolders `1.8` and `1.2`, as `1.10` is superior to both `1.2` and `1.8`

# How do I run this tool in my CI/CD environment?

Just use the below three lines, either at the beginning or at the end of the build:

## Commandline

### Dry Run

```
cd <maven-repository>
./maven-repository-cleaner.sh
```

### Real Execution

```
cd <maven-repository>
./maven-repository-cleaner.sh -y
```

## Script Integration

```
cd <maven-repository>
wget -S -N https://raw.githubusercontent.com/the-oglow/maven-repository-cleaner/1.00.00/maven-repository-cleaner.sh
chmod +x maven-repository-cleaner.sh
./maven-repository-cleaner.sh -y
```

# Does the tool have limitations?

Only **ONE** limitation:

1. The tool believes, for example, that the version `1.1` is older than the version `1.1-alpha-2`

# What is the license?

This forked tool is still licensed under the MIT License.

# Project Status

[![Quality Gate](https://sonarcloud.io/images/project_badges/sonarcloud-black.svg)](https://sonarcloud.io/dashboard?id=the-oglow_maven-repository-cleaner)

## Quality Information

[![Quality Gate](https://sonarcloud.io/api/project_badges/quality_gate?project=the-oglow_maven-repository-cleaner)](https://sonarcloud.io/dashboard?id=the-oglow_maven-repository-cleaner)
[![Codacy Scan Status](https://img.shields.io/codacy/grade/f5ea3eed6b194c398697fef30d7b8672?logo=codacy&style=plastic)](https://www.codacy.com/gh/the-oglow/maven-repository-cleaner)

## Build Information

[![Pipeline status on main branch](https://img.shields.io/github/workflow/status/The-oGlow/maven-repository-cleaner/Build/main?label=main&logo=github&style=plastic)](https://github.com/The-oGlow/maven-repository-cleaner/actions/workflows/build.yml?query=branch%3Amain)

# Test Information

NOTE: **_No tests in this project!_**
