# Gradle
推荐使用本地配置的gradle,在idea中配置本地gradle位置，并保存更改即可
- gradle阿里官方库配置build.gradle
```java
repositories {
    maven {
      url 'https://maven.aliyun.com/repository/public/'
    }
    mavenLocal()
    mavenCentral()
  }
```
- 注意gradle和java-jdk的匹配版本

