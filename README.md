# public-resource

1. `gradle.properties` 생성
  - references: [gradle.properties][gradle.properties]
3. 최상위 gradle 파일에 아래와 같이 설정 

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
    version '0.0.1'
}
```

<!-- external links --> 
[gradle.properties]: https://github.com/huraypositive/core-platform-team/blob/main/gradle.properties
