### Maven

### 第一章 为什么使用Maven

- 获取jar包

  - 使用Maven之前，自行在网络中下载jar包，效率较低。如【谷歌、百度、CSDN....】
  - 使用Maven之后，统一在一个地址下载资源jar包【阿里云镜像服务器等...】

- 添加jar包

  - 使用Maven之前，将jar复制到项目工程中，jar包添加到项目中，相对浪费存储空间
  - 使用Maven之后，jar包统一存储Maven本地仓库，使用坐标方式将jar包从仓库引入到项目中

  ![image-20220320091431579](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20220320091431579.png)

- 使用Maven便于解决jar包**冲突及依赖**问题

### 第二章 什么是Maven

- Maven字面意：专家、内行
- Maven是一款自动化构建工具，专注服务于Java平台的**项目构建**和**依赖管理**。
- 依赖管理：jar之间的依赖关系，jar包管理问题统称为依赖管理
- **项目构建**：项目构建不等同于项目创建
  - 项目构建是一个过程【7步骤组成】，项目创建是瞬间完成的
    1. 清理：mvn clean
    2. 编译：mvn compile
    3. 测试：mvn test
    4. 报告：
    5. 打包：mvn package
    6. 安装：mvn install
    7. 部署：

### 第三章 Maven基本使用

#### 3.1 Maven准备

> 注意：IDEA2019.1.x 最高支持Maven的3.6.0

- 下载地址：http://maven.apache.org/
- Maven底层使用Java语言编写的，所有需要配置JAVA_HOME环境变量及Path
- 将Maven解压**非中文无空格**目录下
- 配置**MAVEN_HOME**环境变量及Path
- 输入【cmd】,进入命令行窗口，输入**【mvn   -v】** ，检查Maven环境是否搭建成功

#### 3.2 Maven基本配置

- Maven配置文件位置：maven根目录/conf/settings.xml

- 设置本地仓库【默认：C:/用户家目录/.m2/repository】

  ```xml
  <!-- localRepository
     | The path to the local repository maven will use to store artifacts.
     |
     | Default: ${user.home}/.m2/repository
    <localRepository>/path/to/local/repo</localRepository>
    -->
    <localRepository>E:\SG_220106\LocalRepository</localRepository>
  ```

- 设置阿里云镜像服务器

  ```xml
  <mirrors>
      <!-- mirror
       | Specifies a repository mirror site to use instead of a given repository. The repository that
       | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
       | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
       |
      <mirror>
        <id>mirrorId</id>
        <mirrorOf>repositoryId</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://my.repository.com/repo/path</url>
      </mirror>
       -->
  	 <mirror>
          <id>nexus-aliyun</id>
          <mirrorOf>central</mirrorOf>
          <name>Nexus aliyun</name>
          <url>http://maven.aliyun.com/nexus/content/groups/public</url>
      </mirror>
    </mirrors>
  ```

- 设置使用JDK版本【1.8|JDK8】

  ```xml
  <profiles>
  <profile>
        <id>jdk-1.8</id>
        <activation>
          <activeByDefault>true</activeByDefault>
          <jdk>1.8</jdk>
        </activation>
        <properties>
          <maven.compiler.source>1.8</maven.compiler.source>
          <maven.compiler.target>1.8</maven.compiler.target>
          <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
        </properties>
      </profile>
    </profiles>
  ```

#### 3.3 Maven之Helloworld

> 约束>配置>代码

- Maven工程目录结构约束
  - 项目名
    - src【书写源代码】
      - main【书写主程序代码】
        - java【书写java源代码】
        - resources【书写配置文件代码】
      - test【书写测试代码】
        - java【书写测试代码】
    - pom.xml【书写Maven配置】

- 测试步骤
  - **进入项目名根目录【在根目标输入cmd即可】**
  - mvn clean 
  - mvn compile
  - mvn test-compile
  - mvn test
  - mvn package
  - mvn install

### 第四章 Maven及Idea的相关应用

#### 4.1 将Maven整合到IDEA中

![image-20220320104957163](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20220320104957163.png)

![image-20220320105010404](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20220320105010404.png)

#### 4.2 在IDEA中新建Maven工程

![image-20220320113913242](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20220320113913242.png)

![image-20220320113928189](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20220320113928189.png)



### 第五章 Maven核心概念

#### 5.1 Maven的POM

- POM全称：Project Object Model【项目对象模型】，将项目封装为对象模型，便于使用Maven管理【构建】项目

- pom.xml常用标签

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <!--    设置父工程坐标-->
      <parent>
          <artifactId>maven_demo</artifactId>
          <groupId>com.atguigu</groupId>
          <version>1.0-SNAPSHOT</version>
      </parent>
      <modelVersion>4.0.0</modelVersion>
  
      <artifactId>maven_helloworld</artifactId>
  
      <dependencies>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
              <scope>test</scope>
          </dependency>
      </dependencies>
  </project>
  ```

#### 5.2 Maven约定的目录结构

- 项目名
  - src【书写java源代码】
    - main【书写java主程序代码】
      - java【书写java代码】
      - resources【书写配置文件代码】
    - test【书写测试代码】
      - java【书写测试java代码】
  - pom.xml【书写配置文件代码】
  - target【编译后目录结构】

#### 5.3 Maven生命周期

- Maven生命周期：按照顺序执行各个命令，Maven生命周期包含以下三个部分组成
  - Clean LifeCycle：在进行真正的构建之前进行一些清理工作。
  - **Default LifeCycle：构建的核心部分，编译，测试，打包，安装，部署等等。**
  - Site LifeCycle：生成项目报告，站点，发布站点。

![image-20220320143031010](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20220320143031010.png)

#### 5.4 Maven插件和目标

- 插件：插件本质是由jar包和配置文件组成
- 目标：每个插件都能实现多个功能，每个功能就是一个插件目标。

#### 5.5 Maven的仓库【重要】

- 仓库分类
  - 本地仓库：为当前计算机提供maven服务
  - 远程仓库：为其他计算机也可以提供maven服务
    - 私服：架设在当前局域网环境下，为当前局域网范围内的所有Maven工程服务。
    - 中央仓库：架设在Internet上，为全世界所有Maven工程服务。
    - 中央仓库的镜像：架设在各个大洲，为中央仓库分担流量。减轻中央仓库的压力，同时更快的响应用户请求。
- 仓库中的文件类型【jar包】
  - Maven的插件
  - 第三方框架或工具的jar包
  - 自己研发的项目或模块

#### 5.6 Maven的坐标【重要】

- **作用：使用坐标引入jar包**

- 坐标由g-a-v组成

  [1]**groupId**：公司或组织的域名倒序+当前项目名称

  [2]**artifactId**：当前项目的模块名称

  [3]**version**：当前模块的版本

- 注意

  - g-a-v：本地仓库jar包位置
  - a-v：jar包全名

- 坐标应用

  - **坐标参考网址：http://mvnrepository.com**

  - 语法，示例

    ```xml
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    
        <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>
    
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.17</version>
        </dependency>
    </dependencies>
    ```

### 第六章 Maven的依赖管理

#### 6.1 依赖范围

- 依赖语法：\<scope>
  - compile【默认值】：在main、test、Tomcat【服务器】下均有效。
  - test：只能在test目录下有效
    - junit
  - provided：在main、test下均有效，Tomcat【服务器】无效。
    - servlet-api

#### 6.2 依赖传递性

- **路径最短者有先【就近原则】**
- **先声明者优先**

- 注意：Maven可以自动解决jar包之间的依赖问题

### 第七章 Maven中统一管理版本号

- 语法

  ```xml
  <properties>
      <spring-version>5.3.17</spring-version>
  </properties>
  <dependencies>
      <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-beans</artifactId>
              <version>${spring-version}</version>
      </dependency>
  </dependencies>
  ```

### 第七章 Maven的继承

#### 7.1 为什么需要继承

- 如子工程大部分都共同使用jar包，可以提取父工程中，使用【继承原理】在子工程中使用
- 父工程打包方式，必须是pom方式

#### 7.2 Maven继承方式一

- 在父工程中的pom.xml中导入jar包，在子工程中统一使用。【所有子工程强制引入父工程jar包】

- 示例代码

  ```xml
  <packaging>pom</packaging>
  <dependencies>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

#### 7.3 Maven继承方式二

- 在父工程中导入jar包【pom.xml】

  ```xml
  <packaging>pom</packaging>
  <dependencyManagement>
      <dependencies>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
              <scope>test</scope>
          </dependency>
      </dependencies>
  </dependencyManagement>
  ```

- 在子工程引入父工程的相关jar包

  ```xml
  <parent>
      <artifactId>maven_demo</artifactId>
      <groupId>com.atguigu</groupId>
      <version>1.0-SNAPSHOT</version>
      <relativePath>../pom.xml</relativePath>
  </parent>
   <dependencies>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
          </dependency>
  </dependencies>
  ```

- **注意：在子工程中，不能指定版本号**

### 第八章 Maven的聚合

- 为什么使用Maven的聚合

  - 优势：只要将子工程聚合到父工程中，就可以实现效果：安装或清除父工程时，子工程会进行同步操作。
  - 注意：Maven会按照依赖顺序自动安装子工程

- 语法

  ```xml
  <modules>
      <module>maven_helloworld</module>
      <module>HelloFriend</module>
      <module>MakeFriend</module>
  </modules>
  ```



