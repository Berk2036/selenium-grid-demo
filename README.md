# Project Setup Guide

## 1. Add Dependencies

To set up the project, add the following dependencies to your `pom.xml`:

### Required Dependencies:


- **Java-Selenium**:
  ```xml
  <dependency>
      <groupId>org.seleniumhq.selenium</groupId>
      <artifactId>selenium-java</artifactId>
      <version>4.26.0</version>
  </dependency>
  ```

- **Cucumber JUnit**:
    ```xml
    <dependency>
      <groupId>io.cucumber</groupId>
      <artifactId>cucumber-junit</artifactId>
      <version>7.3.2</version>
      <scope>test</scope>
  </dependency>
  ```
- **Cucumber JUnit**:
    ```xml
   <dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>7.3.2</version>
  </dependency>
  ```
 ## 2. Add Plugins
 
 Add the following plugins to your pom.xml:

 - **Cucumber JUnit**:
      ```xml
       <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.0.0-M5</version>
        <configuration>
            <includes>
                <include>**/CukesRunner*.java</include>
            </includes>
        </configuration>
     </plugin>
   ```
## 3. Create configuration.properties

## 4. Create Folders and Files
### Project Structure

    src/
    ├── main/
    │   └── java/
    │       └── 
    └── test/
    │   └── java/
    │   │   └── beQualified/
    │   │       ├── pages/        # Page Object Models
    │   │       ├── runners       # Cukesrunner
    │   │       ├── steps/        # Step Definitions for Cucumber
    │   │       └── utilities/    # Utility classes
    │   └── resources/
    │           └── features/     # Cucumber Feature Files
    │   
    └── configuration.properties  # to store configuration parameters 


   ## 5. Create Packages

   Organize your code by creating the following packages:
   - utilities
   - pages
   - runners
   - step_definitions

## 6.Create Utility Classes

**ConfigurationReader.java**
  ```java
    import java.io.FileInputStream;
    import java.io.IOException;
    import java.util.Properties;
    
    public class ConfigurationReader {
        private static Properties properties;
    
        static {
            try (FileInputStream file = new FileInputStream("configuration.properties")) {
                properties = new Properties();
                properties.load(file);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    
        public static String get(String keyName) {
            return properties.getProperty(keyName);
        }
    }
  ```
**Driver.java**
   ```java
      import org.openqa.selenium.WebDriver;
      import org.openqa.selenium.chrome.ChromeDriver;
      
      public class Driver {
          private static WebDriver driver;
      
          private Driver() {
          }
      
          public static WebDriver get() {
              if (driver == null) {
                  System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
                  driver = new ChromeDriver();
              }
              return driver;
          }
      }
 ```

**BrowaerUtils.java**
   ```java
     public class BrowserUtils {
        public static void waitFor(int seconds) {
            try {
                Thread.sleep(seconds * 1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
 ```
