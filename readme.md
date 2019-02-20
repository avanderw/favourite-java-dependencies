# favourite-java-dependencies

| library                      | category |
| ---------------------------- | -------- |
| [tinylog.org](#tinylogorg)   | logging  |
| [cucumber.io](#cucumberio)   | testing  |
| [hamcrest.org](#hamcrestorg) | testing  |

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