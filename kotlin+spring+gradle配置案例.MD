最新更新：20191025

## 参考build.gradle的内容：
```groovy
plugins {
    id 'java'
    // 版本是idea自动生成
    id 'org.jetbrains.kotlin.jvm' version '1.3.50'
    // 使用org.jetbrains.kotlin.jvm一样的版本
    id "org.jetbrains.kotlin.plugin.spring" version "1.3.50"
    // 最新版本参考：https://mvnrepository.com/artifact/org.springframework.boot/spring-boot
    id 'org.springframework.boot' version '2.1.9.RELEASE'
    // 最新版本参考：https://plugins.gradle.org/plugin/io.spring.dependency-management
    id "io.spring.dependency-management" version "1.0.8.RELEASE"
}

group 'Goodzhu-Test'
version '1.0-SNAPSHOT'

sourceCompatibility = 1.8

repositories {
    // 阿里的mvn地址，国内使用
    maven { url 'https://maven.aliyun.com/repository/public' }
    mavenCentral()
}

dependencies {
    // 默认的web启动库，版本自动更新
    compile 'org.springframework.boot:spring-boot-starter-web'
    testCompile 'org.springframework.boot:spring-boot-starter-test'

    // idea自动生成
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk8"
    testCompile group: 'junit', name: 'junit', version: '4.12'
}

compileKotlin {
    kotlinOptions.jvmTarget = "1.8"
}
compileTestKotlin {
    kotlinOptions.jvmTarget = "1.8"
}
```