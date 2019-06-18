# Dependency

## type



## scope

Dependency scope is used to limit the transitivity of a dependency, and also to affect the classpath used for various build tasks.

There are 6 scopes available:

- compile  `default`

- provided

- runtime

- test

- system

  Scope `system` is similar to `provided` except that  `JAR`  need to be provided by `systemPath` since it won't load from maven repository.

- import

  This scope is only supported on a dependency of type `pom` in the `<dependencyManagement>` section. This dependency of type  `pom`  will be replaced with all effective dependencies in it's  `<dependencyManagement>` section.

> Classpath

There are 3 classpaths:

- compile
- runtime
- test

In classpath test, there are also 2 classpaths:

- test compile
- test runtime

Dependencies of different scope are available in different classpaths. 

| scope \ classpath | compile | runtime | test |
| :---------------: | :-----: | :-----: | :--: |
|      compile      |    ✔    |    ✔    |  ✔   |
|     provided      |    ✔    |         |  ✔   |
|      runtime      |         |    ✔    |  ✔   |
|       test        |         |         |  ✔   |

> Transitive

`Dependency` 's  `transitive dependency`  depends on `dependency` that  `dependency `  lays in  `transitive dependency`'s `<dependencies>`  section.

Each of the scopes (except for `import`) affects transitive dependencies in different ways, as is demonstrated in the table below. If a dependency is set to the scope in the left column, of that dependency, `transitive dependency`  with the scope across the top row will result in the scope listed at the intersection. If no scope is listed, it means the dependency will be omitted.

| dependency \ transitive dependency | compile  | provided | runtime  | test |
| :--------------------------------: | :------: | :------: | :------: | :--: |
|              compile               | compile  |    -     | runtime  |  -   |
|              provided              | provided |    -     | provided |  -   |
|              runtime               | runtime  |    -     | runtime  |  -   |
|                test                |   test   |    -     |   test   |  -   |

Dependencies with a scope of `import` do not actually participate in limiting the transitivity of a dependency.