
# SikyliX1 note

## 项目启动

- [sikulix quickstart](http://sikulix.com/quickstart/)
- [安装java jdk](https://blog.csdn.net/Marvin_996_ICU/article/details/106240065)

项目使用Maven 构建Java依赖
于2022/12  建议java是最新的，现在实际运行安装的是 17.0.4.1 2022-08-18 LTS

### mavent
[菜鸟 mavent](https://www.runoob.com/maven/maven-tutorial.html)
固定的项目目录结构
依赖JDK环境
安装mavent 配置环境变量

[pom](https://www.runoob.com/maven/maven-pom.html)
./pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
  ~ Copyright (c) 2010-2021, sikuli.org, sikulix.com - MIT license
  -->

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <!-- 公司或者组织的唯一标志，并且配置时生成的路径也是由此生成， 如com.companyname.project-group，maven会将该项目打成的jar包放本地路径：/com/companyname/project-group -->
  <groupId>com.sikulix</groupId>
  <!-- 项目的唯一ID，一个groupId下面可能多个项目，就是靠artifactId来区分的 -->
  <artifactId>sikulix</artifactId>
  <!-- 版本号 -->
  <version>2.1.0-SNAPSHOT</version>
  <!--项目产生的构件类型，例如jar、war、ear、pom。插件可以创建他们自己的构件类型，所以前面列的不是全部构件类型 -->
  <packaging>pom</packaging>

  <!--模块（有时称作子项目） 被构建成项目的一部分。列出的每个模块元素是指向该模块的目录的相对路径 -->
  <modules>
    <module>API</module>
    <module>IDE</module>
  </modules>
</project>
```
IDE\pom.xml org.sikuli.ide.Sikulix
```xml
<project xmlns = "...">

  <profiles>
    <profile>
      <id>complete-win-jar</id>
      <activation>
        <activeByDefault>false</activeByDefault>
      </activation>
      <build>
        <plugins>
          <plugin>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.1</version>
            <configuration>
              <archive>
                <manifest>
                  <mainClass>org.sikuli.ide.Sikulix</mainClass>
                </manifest>
              </archive>
              <descriptors>
                <descriptor>makeide-win.xml</descriptor>
              </descriptors>
            </configuration>
            <executions>
              <execution>
                <id>make-assembly</id>
                <!--绑定了目标的构建生命周期阶段-->
                <phase>package</phase>
                <!--配置的执行目标 -->
                <goals>
                  <goal>single</goal>
                </goals>
              </execution>
            </executions>
          </plugin>
        </plugins>
      </build>
    </profile>
  </profiles>
</project>
```
vscode 调试
```json
{
  // 使用 IntelliSense 了解相关属性。 
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Launch ide.Sikulix",
      "request": "launch",
      "mainClass": "org.sikuli.ide.Sikulix",
      "projectName": "sikulixide"
    },
  ]
}
```

```cmd
mvn install # 安装依赖
mvn validate # 验证可用
mvn compile # 编译
mvn Test # 测试
mvn validate # 验证可用
```
