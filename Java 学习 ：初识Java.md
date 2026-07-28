---
tags:
  - Java
创建时间: 2026-07-28
---
***
### 一、Java语言版本

- 2014 年：发布Java SE 8 版本，引入了Lambda表达式、Stream API、新的日期/时间API等重要特性。
- 2018 年：发布Java SE 11 版本，成为LTS 版本（Long-Term Support，长期支持版），移除了一些过时的API，引入了新的HTTP Client API等新特性。
- 2023 年：发布 JavaSE 21 版本，它是一个 LTS 版本。
- 2025 年：发布 JavaSE 25 版本，它也是一个LTS版本。
***
### 二、Java语言的三大分支

Java的三大分支之间存在一定的关系，可以简单概括为：

- Java SE是Java的核心部分，Java EE和Java ME都是在Java SE的基础上进行扩展和定制。
- Java EE是在Java SE的基础上增加了更多的企业级技术，如Servlet、JSP、EJB、JMS、JTA等，用于开发大型企业级应用程序。
- Java ME是在Java SE的基础上进行裁剪和优化，使其适合嵌入式设备和移动设备上的应用程序开发。

总之，Java SE是Java的基础，Java EE和Java ME都是在Java SE的基础上进行扩展和定制，用于不同领域的应用程序开发。
***
### 三、Java语言特性


***
### 四、Java的加载与执行

总体包含两个阶段，编译阶段和运行阶段。这两个阶段可以在不同的操作系统上完成。

- 程序员编写完的 .java 文件是源代码文件，使用 `javac` 命令进行编译，`javac` 命令后跟随 .java 源代码文件的名称。
```bash
javac hello.java
```
- 通过 `javac` 命令生成一个或多个 .class 文件，源代码文件中的一个类对应一个 .class 文件，该文件称为**字节码文件**，它不是**机器码文件**，操作系统无法执行，只有 JVM 才能看懂。

- 通过 `java` 命令调动 JVM 将 .class 字节码文件解释为机器码文件，操作系统才能去执行。`java` 命令后跟随类名。
```bash
java hello
```
