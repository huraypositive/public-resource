# public-resource

1. `gradle.properties` 생성 (example: [gradle.properties][gradle.properties])
1. 최상위 gradle 파일에 아래와 같이 설정 

``` gradle
buildscript {
    apply from: 'https://raw.githubusercontent.com/huraypositive/public-resource/main/gradle/variables.gradle'

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
        classpath("org.sonarsource.scanner.gradle:sonarqube-gradle-plugin:$sonarqubeVersion")
    }
}

allprojects {
    group 'net.huray'
//    group 'io.huray'
    version '0.0.1'
}
```

<!-- external links --> 
[gradle.properties]: https://github.com/huraypositive/core-platform-team/blob/main/gradle.properties
