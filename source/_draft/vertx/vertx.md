---
title: Introduction to Vertx
date: 2017-08-27 17:31:34
categories:
  - Pemrograman
  - Vertx
---

![](/images/vertx.png)

# Membuat project vertx
Struktur folder
```
.
├── pom.xml
├── src
│   └── main
│       └── kotlin
├── target
```
pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.ciazhar</groupId>
    <artifactId>vertx-rest</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <name>vertx-rest</name>
</project>
```
properties
```xml
<properties>
    <main.verticle>com.ciazhar.vertx.rest.MainVerticle</main.verticle>
    <vertx.version>3.4.1</vertx.version>
</properties>
```
dependency
```xml
<dependencies>
    <dependency>
      <groupId>io.vertx</groupId>
      <artifactId>vertx-core</artifactId>
      <version>${vertx.version}</version>
    </dependency>
    <dependency>
      <groupId>io.vertx</groupId>
      <artifactId>vertx-lang-kotlin</artifactId>
      <version>${vertx.version}</version>
    </dependency>
  </dependencies>
```
build
```
<build>
    <pluginManagement>
      <plugins>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.1</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
        <plugin>
          <artifactId>kotlin-maven-plugin</artifactId>
          <groupId>org.jetbrains.kotlin</groupId>
          <version>1.1.0</version>
          <executions>
            <execution>
              <id>compile</id>
              <goals> <goal>compile</goal> </goals>
              <configuration>
                <sourceDirs>
                  <sourceDir>${project.basedir}/src/main/kotlin</sourceDir>
                  <sourceDir>${project.basedir}/src/main/java</sourceDir>
                </sourceDirs>
              </configuration>
            </execution>
            <execution>
              <id>test-compile</id>
              <goals> <goal>test-compile</goal> </goals>
              <configuration>
                <sourceDirs>
                  <sourceDir>${project.basedir}/src/test/kotlin</sourceDir>
                  <sourceDir>${project.basedir}/src/test/java</sourceDir>
                </sourceDirs>
              </configuration>
            </execution>
          </executions>
        </plugin>
      </plugins>
    </pluginManagement>

    <plugins>
      <plugin>
        <artifactId>kotlin-maven-plugin</artifactId>
        <groupId>org.jetbrains.kotlin</groupId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>2.3</version>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
            <configuration>
              <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                  <manifestEntries>
                    <Main-Class>io.vertx.core.Launcher</Main-Class>
                    <Main-Verticle>${main.verticle}</Main-Verticle>
                  </manifestEntries>
                </transformer>
                <transformer implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer">
                  <resource>META-INF/services/io.vertx.core.spi.VerticleFactory</resource>
                </transformer>
              </transformers>
              <artifactSet>
              </artifactSet>
              <outputFile>${project.build.directory}/${project.artifactId}-${project.version}-fat.jar</outputFile>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
```
simple verticle
```kotlin
package vertx

import io.vertx.core.AbstractVerticle
import io.vertx.core.Future

class MainVerticle : AbstractVerticle() {

  override fun start(future: Future<Void>) {
    vertx
      .createHttpServer()
      .requestHandler({
          req -> req
              .response()
              .putHeader("content-type", "text/plain")
              .end("Hello from Vert.x!")
      })
      .listen(8080,{
          result ->
          if(result.succeeded()){
              future.complete()
          }
          else{
              future.fail(result.cause())
          }
      })

  }
}
```
# Testing
dependency
```xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>io.vertx</groupId>
  <artifactId>vertx-unit</artifactId>
  <version>3.0.0</version>
  <scope>test</scope>
</dependency>
```
test
```
@RunWith(VertxUnitRunner.class)
public class MyFirstVerticleTest {

  private Vertx vertx;

  @Before
  public void setUp(TestContext context) {
    vertx = Vertx.vertx();
    vertx.deployVerticle(MyFirstVerticle.class.getName(),
        context.asyncAssertSuccess());
  }

  @After
  public void tearDown(TestContext context) {
    vertx.close(context.asyncAssertSuccess());
  }

  @Test
  public void testMyApplication(TestContext context) {
    final Async async = context.async();

    vertx.createHttpClient().getNow(8080, "localhost", "/",
     response -> {
      response.handler(body -> {
        context.assertTrue(body.toString().contains("Hello"));
        async.complete();
      });
    });
  }
}
```
