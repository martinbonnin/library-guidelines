A collection of very personal guidelines for authoring Kotlin libraries so that I can come back to it and remember why I made those weird choices 2 years from now!

Everything subject to change. This just captures the latest state of the decisions.

# Naming

## Project name

Do:

* unique names
* easy to pronounce
* easy to remember
* names that tell a story

Don't:

* generic names that are easy to forget
* always put a 'K'

**Example**: `Apollo Kotlin MockServer`

## GitHub repository name

Use the project name, possibly with a prefix if disambiguation is required.

Use kebab-case if possible.

**Example**: `apollo-kotlin-mockserver`

## Maven Central Namespace

See [Maven Central documentation](https://central.sonatype.org/register/namespace/)

Either use:

* your reversed domain name (`com.example`)
* or your GitHub namespace (`io.github.myusername`)

**Example**: `com.apollographql`

## Maven Central Group Id

Suffix the [namespace](#maven-central-namespace) with your project name. 

You project name may be simplified if some of its part can be deduced from the context.

**Example**: `com.apollographql.mockserver`

### Discussion

Appending the name of the project to the namespaces allows:

* grouping artifacts that are released together as part of the same GitHub repository. It's not 100% clear why 
* renaming all artifacts in a GitHub repository in a single place when a major version is released

Links
* https://jakewharton.com/java-interoperability-policy-for-major-version-updates/

## Maven Central Artifact Id

Use the name of the artifact or `core` if there is only one artifact and no disambiguation is required.

**Example**: `core`, `runtime`, `mockserver`

## Package Name

Use `${groupId}.${artifactId}` if possible.

**Example**: `com.apollographql.mockserver.core`

### Discussion

There is no 1:1 correspondance between Maven coordinates and a package name. This is both happy and sad. Happy because it makes it possible to substitute a dependency by just changing it (the code stays untouched). Sad because it's impossible to know where to look for a given symbol knowing just its package name.

Some projects successfully use short package names (`okhttp3`). This reads way easier but also makes a global search & replace to update to a major version a bit harder (need to search for both `com.squareup.okhttp3` and `okhttp3`, which may have a few more false positives). Also it similarly breaks the coordinates <--> package name mapping.

## Java 9 Module Name

Use the same as the package name.

**Example**: `com.apollographql.mockserver.core`

Links
* https://mail.openjdk.org/pipermail/jpms-spec-experts/2017-February/000582.html

## Gradle plugin id

One solution would be to not use plugins (!). Just pull the dependency in the classpath and call JVM methods. 

For better or worse, the ecosystem is structured around plugins. Use package name as plugin id if there is only one plugin in the artifact. Else specialize them with a suffix

**Example**: `com.apollographql.apollo`, `com.gradleup.gratatouille.wiring`

# Versioning

* `0.0.0` 
  * pre-release
* `1.0.0-alpha.0`
  * has tests
* `1.0.0-beta.0`
  * has documentation
* `1.0.0-rc.0`
  * stable API
* `1.0.0`
  * no more breaking changes until next major
* `2.0.0-alpha.0`
  * breaking changes
  * has tests
* `2.0.0-beta.0`
  * has documentation
* `2.0.0-rc.0`
  * stable API
* `2.0.0`
  * no more breaking changes until next major

## Type Alias vs fun interface

I'm using fun interfaces for KDoc

Links
* https://kotlinlang.org/docs/fun-interfaces.html#functional-interfaces-vs-type-aliases
* https://youtrack.jetbrains.com/issue/KT-23203


