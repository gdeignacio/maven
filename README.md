# maven
Maven repo

No src. See gh-pages branch.

Append this to pom.xml

```
       <repositories>
           <repository>
             <id>github-gdeignacio-maven-repos</id>
             <name>GitHub gdeignacio Maven Repository</name>
             <url>http://gdeignacio.github.io/maven/maven/</url>
           </repository>
        </repositories>
```

To include src in this repo

```
  <build>
    <plugins>
    
      ...
    
      <plugin>
        <artifactId>maven-deploy-plugin</artifactId>
        <version>2.8.1</version>
        <configuration>
          <altDeploymentRepository>
            internal.repo::default::file://${project.build.directory}/mvn-repo
          </altDeploymentRepository>
        </configuration>
      </plugin>

      <plugin>
        <groupId>com.github.github</groupId>
        <artifactId>site-maven-plugin</artifactId>
        <version>0.12</version> 
        <configuration>
          <!-- git commit message -->
          <message>Maven artifacts for ${project.version}</message> 
          <outputDirectory>${project.build.directory}/mvn-repo</outputDirectory> 
          <noJekyll>true</noJekyll>   
          <!-- remote branch name -->
          <branch>refs/heads/gh-pages</branch> 
          <includes>
            <include>**/*</include>
          </includes>
          <path>maven</path>
          <!-- github repo name -->
          <repositoryName>maven</repositoryName>      
          <!-- github username or organization  -->
          <repositoryOwner>gdeignacio</repositoryOwner>    
          <server>github_gdeignacio_maven</server>
          <merge>true</merge>
          <dryRun>false</dryRun>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>site</goal>
            </goals>
            <phase>deploy</phase>
          </execution>
        </executions>
      </plugin>

    </plugins>
  </build>
  
  <distributionManagement>
    <repository>
      <id>github_gdeignacio_maven</id>
      <name>GitHub gdeignacio Maven Repository</name>
      <url>file://${project.build.directory}/mvn-repo</url>
    </repository>
  </distributionManagement>
  
  
  <!--   HOW TO USE: ADD THIS pom.xml    -->
  <!--
        <repositories>
           <repository>
             <id>github-gdeignacio-maven-repos</id>
             <name>GitHub gdeignacio Maven Repository</name>
             <url>http://gdeignacio.github.io/maven/maven/</url>
           </repository>
        </repositories>
  -->
  ```

<table>
<tr><td>
</td></tr>
</table>
