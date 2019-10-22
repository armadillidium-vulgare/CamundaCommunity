# CamundaCommunity

１．Java
    Oracle JDK 10.0.2    

２．Eclipse
    Version: 2019-09 R (4.13.0)
    Build id: 20190917-1200

３．Eclipse Plugin from Marketplace
    Spring Tools 4 - for Spring Boot(aka Spring Tool Suite 4) 4.4.0 RELEASE
    Buildship Gradle Integration 3.0

４．To start Camunda Server on eclipse
     4-1. Right-click on the top-level of the gradle project.
     4-2. Select context menu "Run As" -> "Run Configurations...".
     4-3. Execute ”bootRun” Task by Gradle Task Configuration.

build.gradle:
<pre>
buildscript {
    ext {
        camundaVersion = '7.7.0'
        springBootVersion = '1.5.9.RELEASE'
        camundaSpringBootVersion = '2.2.0'
    }
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
        classpath "io.spring.gradle:dependency-management-plugin:1.0.4.RELEASE"
    }
}

apply plugin: 'java'
apply plugin: 'org.springframework.boot'
apply plugin: "io.spring.dependency-management"

group = 'sample'
version = '0.0.1-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencyManagement {
    imports {
        mavenBom "org.camunda.bpm:camunda-bom:${camundaVersion}"
        mavenBom "org.springframework.boot:spring-boot-dependencies:${springBootVersion}"
        mavenBom "org.camunda.bpm.extension.springboot:camunda-bpm-spring-boot-starter-bom:${camundaSpringBootVersion}"
    }
}

dependencies {
    compile('org.camunda.bpm.extension.springboot:camunda-bpm-spring-boot-starter-webapp')
    compile('com.h2database:h2')
    testCompile('org.springframework.boot:spring-boot-starter-test')
    if(JavaVersion.current() == JavaVersion.VERSION_1_9) {
        runtime('javax.xml.bind:jaxb-api:2.3.0')
    }
}
</pre>

