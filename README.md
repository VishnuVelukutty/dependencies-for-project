# dependencies-for-project
1. Create a seperate repo 
2. Ensure maven is installed
3. mvn archetype:generate -DgroupId=in.ac.iitb.asc -DartifactId=packages-demo -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
4. Add 
```
	<properties>
		<maven.compiler.source>17</maven.compiler.source>
		<maven.compiler.target>17</maven.compiler.target>
	</properties>

```
to change compiler version 

5. generate a personal access token with following permissions
> api, read_api, read_registry, write_registry

6. create a settings.xml 
```
<settings>
    <servers>
      <server>
        <id>gitlab-maven</id>
        <configuration>
          <httpHeaders>
            <property>
              <name>Private-Token</name>
              <value>${Private-token}</value>
            </property>
          </httpHeaders>
        </configuration>
      </server>
    </servers>
  </settings>
  
```

7. Add the following lines  in pom.xml 

```

	<repositories>
		<repository>
			<id>gitlab-maven</id>
			<url>https://gitlab.iitb.ac.in/api/v4/projects/${Project-id}/packages/maven</url>
		</repository>
	</repositories>
	<distributionManagement>
		<repository>
			<id>gitlab-maven</id>
			<url>https://gitlab.iitb.ac.in/api/v4/projects/${Project-id}/packages/maven</url>
		</repository>
		<snapshotRepository>
			<id>gitlab-maven</id>
			<url>https://gitlab.iitb.ac.in/api/v4/projects/${Project-id}/packages/maven</url>
		</snapshotRepository>
	</distributionManagement>

```

8. run ```maven deploy -s settings.xml```