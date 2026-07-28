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

Java既不是纯解释型语言，也不是纯编译型语言，而是一种混合型语言。它既具备编译型语言的高效性，又具备解释型语言的跨平台性。

- **平台无关性（跨平台性：一次编译到处运行）**：Java语言的程序可以在不同的操作系统和硬件平台上运行，这是因为Java程序被编译成字节码，而不是机器码，字节码可以在任何支持Java虚拟机的平台上运行。 实现原理：不同的操作系统上安装属于自己的Java虚拟机，而Java虚拟机屏蔽了各个操作系统之间的差异，从而做到跨平台。

- **自动垃圾回收机制**：Java语言采用的是垃圾回收机制（Garbage Collection，简称GC），也就是自动内存管理机制。在传统的编程语言中，程序员需要手动分配和释放内存，容易出现内存泄漏和悬挂指针等问题。而Java语言采用的垃圾回收机制可以自动分配和释放内存，避免了这些问题。
***
### 四、Java的加载与执行

总体包含两个阶段，编译阶段和运行阶段。这两个阶段可以在不同的操作系统上完成。

- 程序员编写完的 .java 文件是**源代码文件**，使用 `javac` 命令进行编译，`javac` 命令后跟随 .java 源代码文件的名称。
```bash
javac hello.java
```
- 通过 `javac` 命令生成一个或多个 .class 文件，源代码文件中的一个类对应一个 .class 文件，该文件称为**字节码文件**，它不是**机器码文件**，操作系统无法执行，只有 JVM 才能看懂。

- 通过 `java` 命令调动 JVM 将 .class 字节码文件解释为机器码文件，操作系统才能去执行。`java` 命令后跟随类名。
```bash
java hello
```
***
### 五、JDK、JRE、JVM 的关系

- JDK（Java Development Kit）是Java开发工具包，包含了Java开发所需的所有工具和类库。
- JRE（Java Runtime Environment）是Java运行时环境，包含了Java虚拟机和运行Java程序所需的类库等文件。
- JVM（Java Virtual Machine）是Java虚拟机，是Java程序的运行环境，能够在各种平台上运行Java程序，它将Java字节码解释成本地机器码执行。

包含关系：JDK 包含 JRE 包含 JVM
***
