# jooq-code-gen
作为Java/Kotlin的Web项目的辅助，根据数据库表生成jOOQ相关的类。

# 使用方法

## 克隆仓库

```shell
git clone https://github.com/xyplayman/jooq-code-gen.git
```

## 修改pom.xml

根据实际情况，修改文件中如下一段属性配置。
```xml
<properties>
    <db.url>jdbc:mysql://localhost:3306/demo</db.url>
    <db.user>dbuser</db.user>
    <db.password>dbpass</db.password>
    <db.schema>demo</db.schema>
    <package.name>org.xyplayman.demo.jooq</package.name>
    <target.directory>target/generated-sources/jooq</target.directory>
</properties>
```

pom.xml默认使用的数据库是MySQL。如果项目中使用的数据库是MySQL，则无需做更多修改。如果使用的是PostgreSQL，还有两个地方需要将MySQL的配置替换为PostgreSQL。在pom.xml中搜索PostgreSQL，找到如下所示的两段配置，注释掉其中的MySQL相关配置，并打开PostgreSQL的注释。

第一段
```xml
<dependencies>

    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.19</version>
    </dependency>

    <!-- PostgreSQL -->
    <!--
        <dependency>
          <groupId>org.postgresql</groupId>
          <artifactId>postgresql</artifactId>
          <version>42.2.10</version>
        </dependency>
    -->
</dependencies>
```

第二段
```xml
<database>
    <name>org.jooq.meta.mysql.MySQLDatabase</name>
    <!-- PostgreSQL -->
    <!-- <name>org.jooq.meta.postgres.PostgresDatabase</name> -->
    <includes>.*</includes>
    <excludes></excludes>
    <inputSchema>${db.schema}</inputSchema>
</database>
```

## 运行
```shell
mvn jooq-codegen:generate
```
## 使用
在target目录下找到生成的代码，将代码（包括相关的package目录）复制到实际项目的java目录下。请注意，不要手动修改这些代码！如果改变了数据库的结构，那么要再次生成，重新复制。
