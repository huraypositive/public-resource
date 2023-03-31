# public-resource

1. `gradle.properties` 생성
1. 최상위 gradle 파일에 아래와 같이 설정 

``` gradle
buildscript {
    // https://github.com/huraypositive/public-resource/tree/main/gradle
    ext.buildScriptRootUrl = 'https://raw.githubusercontent.com/huraypositive/public-resource/main/gradle'
    apply from: "$buildScriptRootUrl/variables.gradle"

    ext {
        gsonVersion = "2.9.1"
        javaJwtVersion = "3.19.2"
        libphonenumberVersion = "8.12.57"
        lifelogClientVersion = "0.9.1"
    }

    repositories {
        maven {
            url "${mavenReleasesRepositoryUrl}"
            credentials {
                username System.getenv("MAVEN_USERNAME")
                password System.getenv("MAVEN_PASSWORD")
            }
        }
        mavenCentral()
    }

    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:$springBootVersion")
    }
}
```
