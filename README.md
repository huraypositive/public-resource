# public-resource

1. `gradle.properties` 생성 (example: [gradle.properties][gradle.properties])
1. 최상위 gradle 파일에 아래와 같이 설정 

``` gradle
buildscript {
    // https://github.com/huraypositive/public-resource/tree/main/gradle
    ext.buildScriptRootUrl = 'https://raw.githubusercontent.com/huraypositive/public-resource/main/gradle'
    apply from: "$buildScriptRootUrl/variables.gradle"

    repositories {
        maven {
            url "${mavenHurayRepositoryUrl}"
            credentials {
                username System.getenv("MAVEN_USERNAME")
                password System.getenv("MAVEN_PASSWORD")
            }
        }
    }

    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:$springBootVersion")
    }
}

allprojects {
    group 'net.huray'
//    group 'io.huray'
    version '0.0.1'
}
```

1. (선택) 하위 `subprojects` 공통 설정 

``` gradle
subprojects {
    apply plugin: 'java'
    apply plugin: 'idea'
    apply plugin: 'org.springframework.boot'
    apply plugin: 'io.spring.dependency-management'

    sourceCompatibility = '17'

    repositories {
        maven {
            url "${mavenHurayRepositoryUrl}"
            credentials {
                username System.getenv("MAVEN_USERNAME")
                password System.getenv("MAVEN_PASSWORD")
            }
        }
    }

    dependencyManagement {
        imports {
            mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
        }
    }

    configurations {
        compileOnly {
            extendsFrom annotationProcessor
        }
    }

    dependencies {
        /* Lombok */
        compileOnly 'org.projectlombok:lombok'
        annotationProcessor 'org.projectlombok:lombok'
        testCompileOnly 'org.projectlombok:lombok'
        testAnnotationProcessor 'org.projectlombok:lombok'
    }

    tasks.named('test') {
        useJUnitPlatform()
    }

    task printVersion {
        doLast {
            println project.version
        }
    }
}
```

<!-- external links --> 
[gradle.properties]: https://github.com/huraypositive/core-platform-team/blob/main/gradle.properties
