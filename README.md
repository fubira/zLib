zLib
==========
Updated for 1.13.2.

Helper library for Bukkit plugins development.

For the `master` branch:
 - [builds available here](https://jenkins.carrade.eu/job/zLib/);
 - [JavaDoc autogenerated here](https://jenkins.carrade.eu/job/zLib/javadoc/).


### How to use this library in your plugin?

If you are using Maven to build your plugin, follow these simple steps. Other builds methods are not supported (but you can use them of course).  
Currently, the zLib requires **Java 8** or later and **Bukkit 1.13.2** or later.

#### I'm starting a new plugin

Either create a plugin as usual and add the zLib as explained below, or use [the plugin bootstrap generator](https://github.com/zDevelopers/zLib-CodeGen-Utils#plugins-bootstrap-generator) and answer “yes” when the tool asks if you want to use zLib.

#### I want to add zLib to an existing project

1. Add our Maven repository to your `pom.xml` file.
   
    ```xml
        <repository>
            <id>zDevelopers</id>
            <url>http://maven.carrade.eu/artifactory/snapshots</url>
        </repository>
    ```

2. Add the zLib as a dependency.
   
    ```xml
        <dependency>
            <groupId>fr.zcraft</groupId>
            <artifactId>zlib</artifactId>
            <version>0.99-SNAPSHOT</version>
        </dependency>
    ```
    
3. Add the shading plugin to the build. Replace **`YOUR.OWN.PACKAGE`** with your own package.
    
   ```xml
        <build>
            ...
            <plugins>
                ...
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-shade-plugin</artifactId>
                    <version>2.4</version>
                    <configuration>
                        <artifactSet>
                            <includes>
                                <include>fr.zcraft:zlib</include>
                            </includes>
                        </artifactSet>
                        <relocations>
                            <relocation>
                                <pattern>fr.zcraft.zlib</pattern>
                                <shadedPattern>YOUR.OWN.PACKAGE</shadedPattern>
                            </relocation>
                        </relocations>
                    </configuration>
                    <executions>
                        <execution>
                            <phase>package</phase>
                            <goals>
                                <goal>shade</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
                ...
            </plugins>
            ...
        </build>
   ```
   
4. Build your project as usual, as example with the following command from your working directory, or using an integrated tool from your IDE.
   
   ```bash
   mvn clean install
   ```

You should also update your code so your main class extends [`ZPlugin`](https://jenkins.carrade.eu/job/zLib/javadoc/index.html?fr/zcraft/zlib/core/ZPlugin.html) instead of `JavaPlugin`. No other changes are required. This will allow you to use directly some useful methods to load your plugin's components.  
Check out [the wiki](https://github.com/zDevelopers/zLib/wiki/Installation) for more informations.
