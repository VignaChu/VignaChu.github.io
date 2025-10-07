---
title: Maven初步学习
cover: ../../cover/jichi&jichi.jpg
description: 本文介绍了Maven基本的项目结构与依赖管理

date: 2025-10-05T08:00:00+08:00
lastmod: 2025-10-05T08:00:00+08:00

tags:
  - Java
  - Maven
  - 后端学习
  - Study
categories:
  - Study

math: true
mermaid: true

---

# 杂谈

*由于这几天沉迷泰拉瑞亚，加上作业比较多，所以很长时间都没更新*

最近想写一个简单的JAVA应用，但是需要导入外部包，所以需要用到Maven。

Maven是一个构建工具，可以自动化项目构建、依赖管理、项目信息管理等。



# 项目结构

Maven的项目结构如下：

```tree
a-maven-project/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/
│   │   └── resources/
│   └── test/
│       ├── java/
│       └── resources/
└── target/
```


- `pom.xml`：项目的配置文件，包含了项目的基本信息、依赖管理、插件管理等。*注意：Maven的pom文件大小写敏感，建议都为小写*
- `src/main/java`：项目的源代码，包含了项目的业务逻辑。
- `src/main/resources`：项目的资源文件，包含了配置文件、数据库脚本、前端文件、资源文件、Spring Boot配置文件等。
- `src/test/java`：项目的测试代码，包含了单元测试、集成测试等。
- `src/test/resources`：项目的测试资源文件，包含了测试数据、测试配置文件等。
- `target`：项目的输出目录，包含了编译后的class文件、测试报告、打包后的jar文件等。

# 配置文件

`pom.xml`文件是Maven项目的核心配置文件，包含了项目的基本信息、依赖管理、插件管理等。

## 基本信息
- 头部其他部分:为了让编辑器知道这是Maven的配置文件，不用改这些信息。
- `<modelVersion>`:头声明，表明自己所用的Maven的版本。
- **三维坐标**：`<groupId>`、`<artifactId>`、`<version>`，分别表示项目的组ID、项目的Artifact ID、项目的版本。这三个参数用来**唯一**确定一个项目。其中`<groupId>`通常和包的命名方式相同，`<artifactId>`通常是项目的名称，`<version>`是项目的版本号，后加`-SNAPSHOT`表示开发中的版本，通常不会发布。
- `<properties>`：属性区，用于定义JDK版本、依赖版本、字符集等。子工程能继承父工程的属性并加以新的属性。
- `<dependencies>`：依赖管理区，用于声明项目所依赖的jar包。
- `<plugins>`:插件管理区，用于声明项目所使用的插件。 

# 依赖管理

Maven的依赖管理是重要且有用的功能、通过`pom.xml`文件实现。在`<dependencies>`标签下加入，可以声明项目所依赖的jar包，Maven会自动下载、管理这些jar包。通过`<dependency>`及其内部的三维坐标，可以声明依赖的jar包。

还可以通过`<scope>`块定义依赖关系，一共有四种依赖关系。
| 依赖示例        | scope   | 说明                                                                 |
|-----------------|---------|----------------------------------------------------------------------|
| commons-logging | compile | 编译时需要用到该 jar 包（默认）                                      |
| junit           | test    | 编译 Test 时需要用到该 jar 包                                        |
| mysql           | runtime | 编译时不需要，但运行时需要用到                                       |
| servlet-api     | provided| 编译时需要用到，但运行时由 JDK 或某个服务器提供                      |

某个jar包被Maven下载到本地后不会重复下载，但是`-snapshot`版本会重复下载。

# 插件管理

Maven的插件管理是Maven的强大功能之一，通过插件可以实现很多功能，如编译、打包、发布等。在`<plugins>`标签下加入`<plugin>`，可以声明项目所使用的插件。

大部分的插件都放到`<build>`标签下，如编译插件、打包插件、发布插件等。少部分用于输出报告的插件放到`<reporting>`标签下。

`<plugin>`标签内部同样是三维坐标，`<groupId>`、`<artifactId>`、`<version>`，分别表示插件的组ID、插件的Artifact ID、插件的版本。
此外还有用于添加插件参数的`<configuration>`标签，下面以JAVAFX用于开发和打包的插件为例，展示如何配置插件。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <!-- 定义这是一个Maven项目的配置文件 -->
    <modelVersion>4.0.0</modelVersion>
    <!-- 定义Maven的版本 -->
    <groupId>fun.vignachu.code</groupId>
    <artifactId>MavenTest</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!-- 定义项目的组ID、Artifact ID、版本 -->
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <!-- 定义项目的属性，如JDK版本、字符集等 -->
    <dependencies>
        <!-- 核心依赖 -->
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-controls</artifactId>
            <version>21.0.1</version>
        </dependency>

        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-fxml</artifactId>
            <version>21.0.1</version>
        </dependency>
    </dependencies>
    <!-- 定义项目的插件 -->
    <build>
        <plugins>

            <plugin>
                <groupId>org.openjfx</groupId>
                <artifactId>javafx-maven-plugin</artifactId>
                <version>0.0.8</version>
                <!-- 这里是插件的坐标信息 -->
                <configuration>
                    <mainClass>org.example.App</mainClass>
                </configuration>
                <!-- 这里是插件的参数 -->
            </plugin>
        </plugins>
    </build>
</project>

```

# 参考资料
- [封面图源](https://safebooru.org/index.php?page=post&s=view&id=5138139)

- [廖雪峰的官方网站](https://liaoxuefeng.com/books/java/maven/index.html)