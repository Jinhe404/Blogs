###  第一章 初识Mybatis

#### 1.1 框架概述

- #### 生活中“框架”

  - 买房子
  - 笔记本电脑

- 程序中框架【代码半成品】

  - Mybatis框架：持久化层框架【dao层】
  - SpringMVC框架：控制层框架【Servlet层】
  - Spring框架：全能...

#### 1.2 Mybatis简介

- Mybatis是一个**半自动化**持久化层**ORM**框架
- ORM：Object Relational Mapping【对象  关系  映射】
  - 将Java中的**对象**与数据库中**表**建立**映射关系**，优势：操作Java中的对象，就可以影响数据库中表的数据

- Mybatis与Hibernate对比
  - Mybatis是一个半自动化【需要手写SQL】
  - Hibernate是全自动化【无需手写SQL】

- Mybatis与JDBC对比
  - JDBC中的SQL与Java代码耦合度高
  - Mybatis将SQL与Java代码解耦
- Java POJO（Plain Old Java Objects，普通老式 Java 对象）
  - JavaBean  等同于  POJO

#### 1.3 官网地址

- 文档地址：https://mybatis.org/mybatis-3/
- 源码地址：https://github.com/mybatis/mybatis-3

### 第二章 搭建Mybatis框架

> 导入jar包
>
> 编写配置文件
>
> 使用核心类库

#### 2.1 准备

- 建库建表建约束
- 准备maven工程

#### 2.2 搭建Mybatis框架步骤

1. 导入jar包

   ```xml
   <!--导入MySQL的驱动包-->
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>5.1.37</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>8.0.26</version>
   </dependency>
   
   <!--导入MyBatis的jar包-->
   <dependency>
       <groupId>org.mybatis</groupId>
       <artifactId>mybatis</artifactId>
       <version>3.5.6</version>
   </dependency>
   <!--junit-->
   <dependency>
       <groupId>junit</groupId>
       <artifactId>junit</artifactId>
       <version>4.12</version>
       <scope>test</scope>
   </dependency>
   ```

2. 编写**核心配置文件**【mybatis-config.xml】

   - 位置：resources目标下

   - 名称：推荐使用mybatis-config.xml

   - 示例代码

     ```xml
     <?xml version="1.0" encoding="UTF-8" ?>
     <!DOCTYPE configuration
             PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
             "http://mybatis.org/dtd/mybatis-3-config.dtd">
     
     <configuration>
         <environments default="development">
             <environment id="development">
                 <transactionManager type="JDBC"/>
                 <dataSource type="POOLED">
     <!--                mysql8版本-->
     <!--                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>-->
     <!--                <property name="url" value="jdbc:mysql://localhost:3306/db220106?serverTimezone=UTC"/>-->
     <!--                mysql5版本-->
                     <property name="driver" value="com.mysql.jdbc.Driver"/>
                     <property name="url" value="jdbc:mysql://localhost:3306/db220106"/>
                     <property name="username" value="root"/>
                     <property name="password" value="root"/>
                 </dataSource>
             </environment>
         </environments>
         <!--    设置映射文件路径-->
         <mappers>
             <mapper resource="mapper/EmployeeMapper.xml"/>
         </mappers>
     </configuration>
     ```

3. 书写相关接口及**映射文件**

   - 映射文件位置：resources/mapper

   - 映射文件名称：XXXMapper.xml

   - **映射文件作用：主要作用为Mapper接口书写Sql语句**

     - 映射文件名与接口名一致
     - 映射文件namespace与接口全类名一致
     - 映射文件SQL的Id与接口的方法名一致

   - 示例代码

     ```xml
     <?xml version="1.0" encoding="UTF-8" ?>
     <!DOCTYPE mapper
             PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
             "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
     <mapper namespace="com.atguigu.mybatis.mapper.EmployeeMapper">
         <select id="selectEmpById" resultType="com.atguigu.mybatis.pojo.Employee">
             SELECT
                 id,
                 last_name,
                 email,
                 salary
             FROM
                 tbl_employee
             WHERE
                 id=#{empId}
         </select>
     </mapper>
     ```

4. 测试【SqlSession】

   - 先获取SqlSessionFactory对象
   - 再获取SqlSession对象
   - 通过SqlSession对象获取XXXMapper代理对象
   - 测试

#### 2.3 添加Log4j日志框架

- 导入jar包

  ```xml
  <!-- log4j -->
  <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>1.2.17</version>
  </dependency>
  ```

- 编写配置文件

  - 配置文件名称：log4j.xml

  - 配置文件位置：resources

  - 示例代码

    ```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
    
    <log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
    
        <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
            <param name="Encoding" value="UTF-8" />
            <layout class="org.apache.log4j.PatternLayout">
                <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS} %m  (%F:%L) \n" />
            </layout>
        </appender>
        <logger name="java.sql">
            <level value="debug" />
        </logger>
        <logger name="org.apache.ibatis">
            <level value="info" />
        </logger>
        <root>
            <level value="debug" />
            <appender-ref ref="STDOUT" />
        </root>
    </log4j:configuration>
    ```



### 第三章 Mybatis核心配置详解【mybatis-config.xml】

#### 3.1 核心配置文件概述

- MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息。

#### 3.2 核心配置文件根标签

- 没有实际语义，主要作用：所有子标签均需要设置在跟标签内部

#### 3.3 核心配置文件常用子标签

- properties子标签

  - 作用：定义或引入外部属性文件

  - 示例代码

    ```properties
    #key=value
    db.driver=com.mysql.jdbc.Driver
    db.url=jdbc:mysql://localhost:3306/db220106
    db.username=root
    db.password=root
    ```

    ```xml
    <properties resource="db.properties"></properties>
    
    <environments default="development">
            <environment id="development">
                <transactionManager type="JDBC"/>
                <dataSource type="POOLED">
    <!--                mysql8版本-->
    <!--                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>-->
    <!--                <property name="url" value="jdbc:mysql://localhost:3306/db220106?serverTimezone=UTC"/>-->
    <!--                mysql5版本-->
                    <property name="driver" value="${db.driver}"/>
                    <property name="url" value="${db.url}"/>
                    <property name="username" value="${db.username}"/>
                    <property name="password" value="${db.password}"/>
                </dataSource>
            </environment>
        </environments>
    ```

- settings子标签

  - 作用：这是 MyBatis 中极为重要的调整设置，它们会改变 MyBatis 的运行时行为。 

  - **mapUnderscoreToCamelCase**属性：是否开启驼峰命名自动映射，默认值false，如设置true会自动将

    字段a_col与aCol属性自动映射

    - **注意：只能将字母相同的字段与属性自动映射**

- 类型别名（typeAliases）

  - 作用：类型别名可为 Java 类型设置一个缩写名字。

  - 语法及特点

    ```xml
    <typeAliases>
    <!--        为指定类型定义别名-->
    <!--        <typeAlias type="com.atguigu.mybatis.pojo.Employee" alias="employee"></typeAlias>-->
    <!--        为指定包下所有的类定义别名
                    默认将类名作为别名，不区分大小写【推荐使用小写字母】
    -->
            <package name="com.atguigu.mybatis.pojo"/>
        </typeAliases>
    ```

  - Mybatis自定义别名

    | 别名            | 类型      |
    | --------------- | --------- |
    | _int            | int       |
    | integer或int    | Integer   |
    | string          | String    |
    | list或arraylist | ArrayList |
    | map或hashmap    | HashMap   |

    

- 环境配置（environments）

  - 作用：设置数据库连接环境

  - 示例代码

    ```xml
    <!--    设置数据库连接环境-->
        <environments default="development">
            <environment id="development">
                <transactionManager type="JDBC"/>
                <dataSource type="POOLED">
    <!--                mysql8版本-->
    <!--                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>-->
    <!--                <property name="url" value="jdbc:mysql://localhost:3306/db220106?serverTimezone=UTC"/>-->
    <!--                mysql5版本-->
                    <property name="driver" value="${db.driver}"/>
                    <property name="url" value="${db.url}"/>
                    <property name="username" value="${db.username}"/>
                    <property name="password" value="${db.password}"/>
                </dataSource>
            </environment>
        </environments>
    ```

- mappers子标签

  - 作用：设置映射文件路径

  - 示例代码

    ```xml
    <!--    设置映射文件路径-->
        <mappers>
            <mapper resource="mapper/EmployeeMapper.xml"/>
            <!-- 要求：接口的包名与映射文件的包名需要一致-->
    <!--        <package name="com.atguigu.mybatis.mapper"/>-->
        </mappers>
    ```

- 注意：核心配置中的子标签，是有顺序要求的。

  ![image-20220321153852708](http://rx6zk4j2b.hn-bkt.clouddn.com/blogs/image-20220321153852708.png)

### 第四章 Mybatis映射文件详解

#### 4.1 映射文件概述

- MyBatis 的真正强大在于它的语句映射，这是它的魔力所在。
- 如果拿它跟具有相同功能的 JDBC 代码进行对比，你会立即发现省掉了将近 **95%** 的代码。

#### 4.2 映射文件根标签

- mapper标签
- mapper中的namespace要求与接口的全类名一致

#### 4.3 映射文件子标签

> 子标签共有9个，注意学习其中8大子标签

- insert标签：定义添加SQL
- delete标签：定义删除SQL
- update标签：定义修改SQL
- select标签：定义查询SQL
- sql标签：定义可重用的SQL语句块
- cache标签：设置当前命名空间的缓存配置
- cache-ref标签：设置其他命名空间的缓存配置
- **resultMap标签：**描述如何从数据库结果集中加载对象
  - resultType解决不了的问题，交个resultMap。

#### 4.4 映射文件中常用属性

- resultType：设置期望结果集返回类型【全类名或别名】
  - 注意：如果返回的是集合，那应该设置为集合包含的类型，而不是集合本身的类型。 
  - resultType 和 resultMap 之间只能同时使用一个。

#### 4.5 获取主键自增数据

- useGeneratedKeys：启用主键生成策略
- keyProperty：设置存储属性值

#### 4.6 获取数据库受影响行数

- 直接将接口中方法的返回值设置为int或boolean即可
  - int：代表受影响行数
  - boolean
    - true：表示对数据库有影响
    - false：表示对数据库无影响

### 第五章 Mybatis中参数传递问题

#### 5.1 单个普通参数

- 可以任意使用：参数数据类型、参数名称不用考虑

#### 5.2 多个普通参数

- Mybatis底层封装Map结构，封装key为param1、param2....【支持：arg0、arg1、...】

#### 5.3 命名参数

- 语法：

  - @Param(value="参数名")
  - @Param("参数名")

- 位置：参数前面

- 注意：

  - 底层封装Map结构
  - 命名参数，依然支持参数【param1,param2,...】

- 示例代码

  ```java
  /**
   * 通过员工姓名及薪资查询员工信息【命名参数】
   * @return
   */
  public List<Employee> selectEmpByNamed(@Param("lName")String lastName,
                                         @Param("salary") double salary);
  ```

  ```xml
  <select id="selectEmpByNamed" resultType="employee">
      SELECT
          id,
          last_name,
          email,
          salary
      FROM
          tbl_employee
      WHERE
          last_name=#{param1}
      AND
          salary=#{param2}
  </select>
  ```

- 源码分析

  - MapperMethod对象：142行代码【命名参数底层代码入口】

  - **命名参数底层封装map为ParamMap，ParamMap继承HashMap**

  - ParamNameResolver对象：130行代码，命名参数底层实现逻辑

    ```java
    //130行
    final Map<String, Object> param = new ParamMap<>();
    int i = 0;
    for (Map.Entry<Integer, String> entry : names.entrySet()) {
      param.put(entry.getValue(), args[entry.getKey()]);
      // add generic param names (param1, param2, ...)
      final String genericParamName = GENERIC_NAME_PREFIX + (i + 1);
      // ensure not to overwrite parameter named with @Param
      if (!names.containsValue(genericParamName)) {
        param.put(genericParamName, args[entry.getKey()]);
      }
      i++;
    }
    return param;
    ```

#### 5.4 POJO参数

- Mybatis支持POJO【JavaBean】入参，参数key是POJO中属性

#### 5.5 Map参数

- Mybatis支持直接Map入参，map的key=参数key

#### 5.6 Collection|List|Array等参数

- 参数名：collection、list、array

### 第六章 Mybatis参数传递【#与$区别】

#### 6.1 回顾JDBC

- DriverManager
- Connection
- **Statement**：执行SQL语句，入参使用SQL【String】拼接方式
- **PreparedStatement**执行SQL语句【预编译SQL】，入参使用占位符方式
- ResultSet

#### 6.2 #与$区别

- 【#】底层执行SQL语句的对象，使用**PreparedStatementd**，预编译SQL，防止SQL注入安全隐患，相对比较安全。
- 【$】底层执行SQL语句的对象使用**Statement**对象，未解决SQL注入安全隐患，相对不安全。

#### 6.3 #与$使用场景

> 查询SQL：select col,col2 from table1 where col=? and col2=?  group by ?, order by ?  limit ?,?

- #使用场景，sql占位符位置均可以使用#

- $使用场景，#解决不了的参数传递问题，均可以交给$处理【如：form 动态化表名】

  ```java
  /**
   * 测试$使用场景
   */
  public List<Employee> selectEmpByDynamitTable(@Param("tblName") String tblName);
  ```

  ```xml
  <select id="selectEmpByDynamitTable" resultType="employee">
      SELECT
          id,
          last_name,
          email,
          salary
      FROM
          ${tblName}
  </select>
  ```

### 第七章 Mybatis查询中返回值四种情况

#### 7.1 查询单行数据返回单个对象

```java
/**
 * 通过id获取员工信息
 */
public Employee selectEmpById(int empId);
```

```xml
<select id="selectEmpById" resultType="employee">
    SELECT
        id,
        last_name,
        email,
        salary
    FROM
        tbl_employee
    WHERE
        id=#{empId}
</select>
```

#### 7.2 查询多行数据返回对象的集合

```java
/**
 * 查询所有员工信息
 */
public List<Employee> selectAllEmps();
```

```xml
<select id="selectAllEmps" resultType="employee">
    SELECT
        id,
        last_name,
        email,
        salary
    FROM
        tbl_employee
</select>
```

- 注意：如果返回的是集合，那应该设置为**集合包含的类型**，而不是集合本身的类型。 

#### 7.3 查询单行数据返回Map集合

- Map<String key,Object value>

  - 字段作为Map的key，查询结果作为Map的Value

- 示例代码

  ```java
  /**
   * 查询单行数据返回Map集合
   * @return
   */
  public Map<String,Object> selectEmpReturnMap(int empId);
  ```

  ```xml
  <!--    查询单行数据返回Map集合-->
  <select id="selectEmpReturnMap" resultType="map">
      SELECT
          id,
          last_name,
          email,
          salary
      FROM
      	tbl_employee
      WHERE
      	id=#{empId}
  </select>
  ```

#### 7.4 查询多行数据返回Map集合

- Map<Integer key,Employee value>

  - 对象的id作为key
  - 对象作为value

- 示例代码

  ```java
  /**
   * 查询多行数据返回Map
   * Map<Integer,Object>
   * Map<Integer,Employee>
   *      对象Id作为：key
   *      对象作为：value
   * @return
   */
  @MapKey("id")
  public Map<Integer,Employee> selectEmpsReturnMap();
  ```

  ```xml
  <select id="selectEmpsReturnMap" resultType="map">
      SELECT
          id,
          last_name,
          email,
          salary
      FROM
          tbl_employee
  </select>
  ```

### 第八章 Mybatis中自动映射与自定义映射

> 自动映射【resultType】
>
> 自定义映射【resultMap】

#### 8.1 自动映射与自定义映射

- 自动映射【resultType】：指的是自动将表中的字段与类中的属性进行关联映射
  - 自动映射解决不了两类问题	
    - **多表连接查询时，需要返回多张表的结果集**
    - 单表查询时，不支持驼峰式自动映射【不想为字段定义别名】
- 自定义映射【resultMap】：自动映射解决不了问题，交给自定义映射
- 注意：resultType与resultMap只能同时使用一个

#### 8.2 自定义映射-级联映射

```xml
<!--    自定义映射 【员工与部门关系】-->
<resultMap id="empAndDeptResultMap" type="employee">
    <!--  定义主键字段与属性关联关系 -->
    <id column="id" property="id"></id>
    <!--  定义非主键字段与属性关联关系-->
    <result column="last_name" property="lastName"></result>
    <result column="email" property="email"></result>
    <result column="salary" property="salary"></result>
    <!--        为员工中所属部门，自定义关联关系-->
    <result column="dept_id" property="dept.deptId"></result>
    <result column="dept_name" property="dept.deptName"></result>
</resultMap>
<select id="selectEmpAndDeptByEmpId" resultMap="empAndDeptResultMap">
   SELECT
        e.`id`,
        e.`email`,
        e.`last_name`,
        e.`salary`,
        d.`dept_id`,
        d.`dept_name`
    FROM
        tbl_employee e,
        tbl_dept d
    WHERE
        e.`dept_id` = d.`dept_id`
    AND
        e.`id` = #{empId}
</select>
```

#### 8.3 自定义映射-association映射

- 特点：解决一对一映射关系【一对多】

- 示例代码

  - ```xml
    <!--    自定义映射 【员工与部门关系】-->
    <resultMap id="empAndDeptResultMapAssociation" type="employee">
        <!--  定义主键字段与属性关联关系 -->
        <id column="id" property="id"></id>
        <!--  定义非主键字段与属性关联关系-->
        <result column="last_name" property="lastName"></result>
        <result column="email" property="email"></result>
        <result column="salary" property="salary"></result>
        <!--        为员工中所属部门，自定义关联关系-->
        <association property="dept"
                    javaType="com.atguigu.mybatis.pojo.Dept">
            <id column="dept_id" property="deptId"></id>
            <result column="dept_name" property="deptName"></result>
        </association>
    </resultMap>
    ```

#### 8.4 自定义映射-collection映射

- 示例代码

  ```java
  /**
   * 通过部门id获取部门信息，及部门所属员工信息
   */
  public Dept selectDeptAndEmpByDeptId(int deptId);
  ```

  ```xml
  <resultMap id="deptAndempResultMap" type="dept">
      <id property="deptId" column="dept_id"></id>
      <result property="deptName" column="dept_name"></result>
      <collection property="empList"
                  ofType="com.atguigu.mybatis.pojo.Employee">
          <id column="id" property="id"></id>
          <result column="last_name" property="lastName"></result>
          <result column="email" property="email"></result>
          <result column="salary" property="salary"></result>
      </collection>
  </resultMap>
  <select id="selectDeptAndEmpByDeptId" resultMap="deptAndempResultMap">
      SELECT
          e.`id`,
          e.`email`,
          e.`last_name`,
          e.`salary`,
          d.`dept_id`,
          d.`dept_name`
      FROM
          tbl_employee e,
          tbl_dept d
      WHERE
          e.`dept_id` = d.`dept_id`
      AND
          d.dept_id = #{deptId}
  </select>
  ```

#### 8.5 ResultMap相关标签及属性

- resultMap标签：自定义映射标签
  - id属性：定义唯一标识
  - type属性：设置映射类型

- resultMap子标签
  - id标签：定义主键字段与属性关联关系
  - result标签：定义非主键字段与属性关联关系
    - column属性：定义表中字段名称
    - property属性：定义类中属性名称
  - association标签：定义一对一的关联关系
    - property：定义关联关系属性
    - javaType：定义关联关系属性的类型
    - select：设置分步查询SQL全路径
    - colunm：设置分步查询SQL中需要参数
  - collection标签：定义一对多的关联关系
    - property：定义一对一关联关系属性
    - ofType：定义一对一关联关系属性类型

#### 8.6 Mybatis中分步查询

- 为什么使用分步查询【分步查询优势】？
  - 将多表连接查询，改为【分步单表查询】，从而提高程序运行效率



#### 8.7 Mybatis延迟加载【懒加载】

- 需要时加载，不需要暂时不加载

  - 优势：提升程序运行效率

- 语法

  - 全局设置

    ```xml
    <!-- 开启延迟加载 -->
    <setting name="lazyLoadingEnabled" value="true"/>
    <!-- 设置加载的数据是按需加载3.4.2及以后的版本该步骤可省略-->
    <setting name="aggressiveLazyLoading" value="false"/>
    ```

  - 局部设置

    - fetchType

      - eager：关闭局部延迟加载
      - lazy：开启局部延迟加载

    - 示例代码

      ```xml
      <association property="dept"
                  select="com.atguigu.mybatis.mapper.DeptMapper.selectDeptByDeptId"
                  column="dept_id"
                  fetchType="eager">
      </association>
      ```



































