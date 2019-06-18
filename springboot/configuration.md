# Configuration

There are 2 popular configuration files in Spring Boot:

- properties
- yml

Too many configurations lead to confusion in one file, Spring Boot always has solutions.

## properties

Properties can hold multiple files in resources, the default is named `application.properties`, others need to be active.

```properties
spring.profiles.active/include=${profile}
```

Then properties `application-${profile}.properties` is active.

Multiple properties also work with multiple active.

```properties
spring.profiles.active/include=${profile1},${profile2}
```

Then properties `application-${profile1}.properties` and `application-${profile2}.properties` are active.

If the properties file's name doesn't begin with 'application', `@PropertySource` in `Application` holds the same active.

```java
@SpringBootApplication
@PropertySource(value = "classpath:${profile}.properties")
public class Application {
	...
}
```

`@PropertySource` can also work with multiple properties.

```java
@SpringBootApplication
@PropertySource(value = {"classpath:${profile1}.properties","classpath:${profile2}.properties"})
public class Application {
	...
}
```

`@PropertySources` is an another annotation.

```java
@SpringBootApplication
@PropertySources({
        @PropertySource(value = "classpath:${profile1}.properties"),
        @PropertySource(value = "classpath:${profile2}.properties")
})
public class Application {
	...
}
```

## yml

Officially, `yaml` is recommended in preference to `yml`, but for historic reasons many Windows programmers are still scared of using extensions with more than three characters, so use `yml` instead.

Familier with `properties` above, `yml` can also be active.

```yml
spring
	profiles
		active/include:${profile}
```

Then `application-${profile}.yml` is active.

Different from `properties`, if `application-${profile}.yml` doesn't exist, `${profile}` in `application.yml` has the same effects.

```yaml
spring
	profiles
		active/include:${profile}
---
spring
	profiles:${profile}
```

Multiple yml also work with multiple active.

```yaml
spring
	profiles
		active/include:${profile1},${profile2}
```

Then `application-${profile1}.yml` and `application-${profile2}.yml` are active.

If `application-${profile}.yml` doesn't exist, `${profile1}` and `${profile2}` in `application.yml` have the same effects.

```yaml
spring
	profiles
		active/include:${profile}
---
spring
	profiles:${profile1}
---
spring
	profiles:${profile2}

```

### JVM System Parameter

The profile names can also be passed in via a JVM system parameter. The profile names passed as the parameter will be activated during application start-up:

```
-Dspring.profiles.active=${profile}

```

## Environment Variable

Profiles can also be activated via the environment variable:

```
export spring_profiles_active=${profile}

```