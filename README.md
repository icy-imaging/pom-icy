# Icy Parent POM

![Maven logo](https://upload.wikimedia.org/wikipedia/commons/5/52/Apache_Maven_logo.svg)

<!-- badges: start -->
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)  
[![Twitter](https://img.shields.io/twitter/follow/Icy_BioImaging?style=social)](https://twitter.com/Icy_BioImaging)  
[![Image.sc forum](https://img.shields.io/badge/discourse-forum-brightgreen.svg?style=flat)](https://forum.image.sc/tag/icy)
<!-- badges: end -->

This is the repository for the Maven configuration of *pom-icy, Icy's Parent POM*, a Maven file for [bioimage analysis software Icy](http://icy.bioimageanalysis.org/) and its plugins, which was developed by members or former members of the [Biological Image Analysis unit at Institut Pasteur](https://research.pasteur.fr/en/team/bioimage-analysis/). This project is licensed under GPL3 license.     
Icy is developed and maintained by [Biological Image Analysis unit at Institut Pasteur](https://research.pasteur.fr/en/team/bioimage-analysis/). The [source code of Icy](https://gitlab.pasteur.fr/bia/icy) is also licensed under a GPL3 license. 

## Description

To know more about how POM file in Maven projects works, you can check those resources:
- [Introduction to Maven](https://icy.bioimageanalysis.org/developer/introduction-to-maven/), an Icy article
- [Introduction to the POM](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html#project-inheritance), Apache Maven Project
- [Maven - Parent and Child POM](https://howtodoinjava.com/maven/maven-parent-child-pom-example/), HowToDoInJava
- [Maven by Example, 6.2. The Simple Parent Project](https://books.sonatype.com/mvnex-book/reference/multimodule-sect-simple-parent.html), Sonatype Nexus

This project centralizes the Maven configuration for Icy as well as its plugins in one file. It will be inherited to the other projects with the `parent` block:
```xml
<parent>
    <artifactId>pom-icy</artifactId>
    <groupId>org.bioimageanalysis.icy</groupId>
    <version>2.1.0</version>
</parent>
```

There is two profiles to facilitate project management:
- `plugin`: Dedicated to Icy plugin development so it includes default dependencies and rules.
  Runs by default `clean` and `package`&ast; goals.
- `library`: Dedicated to plugin library which need dependencies extraction, in which case you define artifact(s) to extract through the `artifact-to-include` property.
  You should always use this profile along the `plugin` profile.

To deploy the project/artefact to the Icy's Nexus repositories just use the `deploy` goal instead. Note that Nexus development repositories are accessible only in Pasteur offices or through the private VPN.
You want to upload on our public repositories and you do not have an account ? Send a mail to [Icy Team,](mailto:icy.team@pasteur.fr) and we will grant you access.
Are you a Pasteur employee ? A connection through PasteurID is coming soon !

To use a profile, you can:
- Run the command in your terminal: `mvn -P<profile-name>`, and to use multiple profiles, `mvn -P<profile-name-1>,<profile-name-2`
- In your IDE:
  - In [IntelliJ](https://www.jetbrains.com/help/idea/work-with-maven-profiles.html#declare_maven_profiles)
  - In [Eclipse](https://www.czetsuyatech.com/2011/11/maven-activate-maven-profile-on-eclipse.html)
- Overriding the profile activation in your project to have it by default: 
```xml
<profiles>
  <profile>
    <id>same-id-as-the-one-to-override</id>
    <activation>
      <activeByDefault>true</activeByDefault>
    </activation>
  </profile>
</profiles>
```
After, you can just run `mvn` or in your IDE without any configuration, and it will do everything for you!

-> To see which profiles are activated, run the command `mvn help:active-profiles` in your terminal.

## Dependency list

To keep a cohesion between Icy and all plugins, we have listed some most used plugins as dependency to others plugins and set its version.

To know them, check the `<properties>` block in the `pom.xml`.

To call them, you need to add the `<dependency>` block as follows:
```xml
<dependency>
  <groupId>org.bioimagenalaysis.icy</groupId>
  <artifactId>name-of-plugin</artifactId>
</dependency>
```

&ast; The `package` phase generate three JARs: one to executable for Icy, a source JAR and a JavaDoc JAR. 

## Citation

Please also cite the Icy software and mention the version of Icy you used (bottom right corner of the GUI or first lines of the Output tab):     
de Chaumont, F. et al. (2012) Icy: an open bioimage informatics platform for extended reproducible research, [Nature Methods](https://www.nature.com/articles/nmeth.2075), 9, pp. 690-696       
http://icy.bioimageanalysis.org    

## Authors

Amandine TOURNAY