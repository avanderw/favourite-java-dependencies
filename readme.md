# favourite-java-dependencies

| library                                    | category |
| ------------------------------------------ | -------- |
| [tinylog.org](#tinylogorg)                 | logging |
| [cucumber.io](#cucumberio)                 | testing |
| [hamcrest.org](#hamcrestorg)               | testing |
| [google/guice](#googleguice)               | dependency injection |
| [square/javapoet](#squarejavapoet)         | code-generation |
| [commons-math](#commons-math)              | math |
| [ronmamo/reflections](#ronmamoreflections) | code-generation |
| [remkop/picocli](#remkoppicocli)           | cli |

## [tinylog.org](https://tinylog.org/)

```java
import org.pmw.tinylog.Logger;

public class Main {
    public static void main(String[] args) {
        Logger.info("Hello world!");
    }
}
```

```xml
<dependency>
  <groupId>org.tinylog</groupId>
  <artifactId>tinylog</artifactId>
  <version>1.3.6</version>
</dependency>
```

## [cucumber.io](https://docs.cucumber.io/)

```gherkin
Feature: Eating too many cucumbers may not be good for you

  Eating too much of anything may not be good for you.

  Scenario: Eating a few is no problem
    Given Alice is hungry 
    When she eats 3 cucumbers
    Then she will be full
```

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java8</artifactId>
    <version>4.2.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-picocontainer</artifactId>
    <version>4.2.1</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-junit</artifactId>
    <version>4.2.0</version>
    <scope>test</scope>
</dependency>
```

## [hamcrest.org](http://hamcrest.org/JavaHamcrest/)

```java
import org.junit.jupiter.api.Test;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.Matchers.*;

public class BiscuitTest {
    @Test
    public void testEquals() {
        Biscuit theBiscuit = new Biscuit("Ginger");
        Biscuit myBiscuit = new Biscuit("Ginger");
        assertThat(theBiscuit, equalTo(myBiscuit));
    }
}
```

```xml
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest</artifactId>
    <version>2.1</version>
    <scope>test</scope>
</dependency>
```

## [google/guice](https://github.com/google/guice/wiki/Motivation)

```java
public static void main(String[] args) {
    Injector injector = Guice.createInjector(new BillingModule());
    BillingService billingService = injector.getInstance(BillingService.class);
    ...
  }
```

```xml
<dependency>
	<groupId>com.google.inject</groupId>
	<artifactId>guice</artifactId>
	<version>4.2.0</version>
</dependency>
```

## [square/javapoet](https://github.com/square/javapoet)

```java
MethodSpec today = MethodSpec.methodBuilder("today")
    .returns(Date.class)
    .addStatement("return new $T()", Date.class)
    .build();

TypeSpec helloWorld = TypeSpec.classBuilder("HelloWorld")
    .addModifiers(Modifier.PUBLIC, Modifier.FINAL)
    .addMethod(today)
    .build();

JavaFile javaFile = JavaFile.builder("com.example.helloworld", helloWorld)
    .build();

javaFile.writeTo(System.out);

//
// Generates
//

package com.example.helloworld;

import java.util.Date;

public final class HelloWorld {
  Date today() {
    return new Date();
  }
}
```

```xml
<dependency>
    <groupId>com.squareup</groupId>
    <artifactId>javapoet</artifactId>
    <version>1.11.1</version>
</dependency>
```

## [commons-math](http://commons.apache.org/proper/commons-math/)

```java
// Get a DescriptiveStatistics instance
DescriptiveStatistics stats = new DescriptiveStatistics();

// Add the data from the array
for( int i = 0; i < inputArray.length; i++) {
        stats.addValue(inputArray[i]);
}

// Compute some statistics
double mean = stats.getMean();
double std = stats.getStandardDeviation();
double median = stats.getPercentile(50);

// random sampling with distribution control
List<Pair<Heart, Double>> hearts = new ArrayList<>();
        hearts.add(new Pair<>(new Heart("bionic"), 0.4));
        hearts.add(new Pair<>(new Heart("diamond"), 0.1));
        hearts.add(new Pair<>(new Heart("cybernetic"), 0.3));
        hearts.add(new Pair<>(new Heart("tissue"), 0.2));
        EnumeratedDistribution<Heart> distribution = new EnumeratedDistribution<>(hearts);
        return distribution.sample();
```

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-math3</artifactId>
    <version>3.6.1</version>
</dependency>
```

## [ronmamo/reflections](https://github.com/ronmamo/reflections)

```java
//scan urls that contain 'my.package', include inputs starting with 'my.package', use the default scanners
Reflections reflections = new Reflections("my.package");

//or using ConfigurationBuilder
new Reflections(new ConfigurationBuilder()
     .setUrls(ClasspathHelper.forPackage("my.project.prefix"))
     .setScanners(new SubTypesScanner(), 
                  new TypeAnnotationsScanner().filterResultsBy(optionalFilter), ...),
     .filterInputsBy(new FilterBuilder().includePackage("my.project.prefix"))
     ...);
	 
//SubTypesScanner
Set<Class<? extends Module>> modules = 
    reflections.getSubTypesOf(com.google.inject.Module.class);
	
//TypeAnnotationsScanner 
Set<Class<?>> singletons = 
    reflections.getTypesAnnotatedWith(javax.inject.Singleton.class);
	
//ResourcesScanner
Set<String> properties = 
    reflections.getResources(Pattern.compile(".*\\.properties"));
	
//MethodAnnotationsScanner
Set<Method> resources =
    reflections.getMethodsAnnotatedWith(javax.ws.rs.Path.class);
Set<Constructor> injectables = 
    reflections.getConstructorsAnnotatedWith(javax.inject.Inject.class);
	
//FieldAnnotationsScanner
Set<Field> ids = 
    reflections.getFieldsAnnotatedWith(javax.persistence.Id.class);
	
//MethodParameterScanner
Set<Method> someMethods =
    reflections.getMethodsMatchParams(long.class, int.class);
Set<Method> voidMethods =
    reflections.getMethodsReturn(void.class);
Set<Method> pathParamMethods =
    reflections.getMethodsWithAnyParamAnnotated(PathParam.class);
	
//MethodParameterNamesScanner
List<String> parameterNames = 
    reflections.getMethodParamNames(Method.class)
	
//MemberUsageScanner
Set<Member> usages = 
    reflections.getMethodUsages(Method.class)
```

```xml
<dependency>
    <groupId>org.reflections</groupId>
    <artifactId>reflections</artifactId>
    <version>0.9.11</version>
</dependency>
```

## [remkop/picocli](https://github.com/remkop/picocli)

```java
import picocli.CommandLine;
import picocli.CommandLine.Option;
import picocli.CommandLine.Parameters;
import java.io.File;

@Command(name = "example", mixinStandardHelpOptions = true, version = "Picocli example 3.0")
public class Example implements Runnable {
    @Option(names = { "-v", "--verbose" }, description = "Verbose mode. Helpful for troubleshooting. " +
                                                         "Multiple -v options increase the verbosity.")
    private boolean[] verbose = new boolean[0];

    @Parameters(arity = "1..*", paramLabel = "FILE", description = "File(s) to process.")
    private File[] inputFiles;
    
    public void run() {
        if (verbose.length > 0) {
            System.out.println(inputFiles.length + " files to process...");
        }
        if (verbose.length > 1) {
            for (File f : inputFiles) {
                System.out.println(f.getAbsolutePath());
            }
        }
    }
    
    public static void main(String[] args) {
        CommandLine.run(new Example(), args);
    }
}
```

```xml
<dependency>
  <groupId>info.picocli</groupId>
  <artifactId>picocli</artifactId>
  <version>3.9.5</version>
</dependency>
```