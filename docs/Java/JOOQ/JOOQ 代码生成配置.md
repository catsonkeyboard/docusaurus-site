---
sidebar_position: 1
---

### configuration配置

```xml
<configuration>
  <!-- 跳过生成,可以配置变量,在使用maven编译项目的时候动态设置 -->
  <skip>false</skip>
  <!-- Configure the database connection here -->
  <jdbc>
    <driver>org.postgresql.Driver</driver>
    <url>jdbc:postgresql://[ip]:[port]/[database]?[your jdbc connection parameters]</url>
    <user>[your database user]</user>
    <password>[your database password]</password>

    <!-- You can also pass user/password and other JDBC properties in the optional properties tag: -->
    <properties>
      <property><key>user</key><value>[db-user]</value></property>
      <property><key>password</key><value>[db-password]</value></property>
    </properties>
  </jdbc>

  <generator>
    <database>
      <!-- The database dialect from jooq-meta. Available dialects are
           named org.jooq.meta.[database].[database]Database.

           Natively supported values are:

               org.jooq.meta.ase.ASEDatabase
               org.jooq.meta.auroramysql.AuroraMySQLDatabase
               org.jooq.meta.aurorapostgres.AuroraPostgresDatabase
               org.jooq.meta.cockroachdb.CockroachDBDatabase
               org.jooq.meta.db2.DB2Database
               org.jooq.meta.derby.DerbyDatabase
               org.jooq.meta.firebird.FirebirdDatabase
               org.jooq.meta.h2.H2Database
               org.jooq.meta.hana.HANADatabase
               org.jooq.meta.hsqldb.HSQLDBDatabase
               org.jooq.meta.ignite.IgniteDatabase
               org.jooq.meta.informix.InformixDatabase
               org.jooq.meta.ingres.IngresDatabase
               org.jooq.meta.mariadb.MariaDBDatabase
               org.jooq.meta.mysql.MySQLDatabase
               org.jooq.meta.oracle.OracleDatabase
               org.jooq.meta.postgres.PostgresDatabase
               org.jooq.meta.redshift.RedshiftDatabase
               org.jooq.meta.snowflake.SnowflakeDatabase
               org.jooq.meta.sqldatawarehouse.SQLDataWarehouseDatabase
               org.jooq.meta.sqlite.SQLiteDatabase
               org.jooq.meta.sqlserver.SQLServerDatabase
               org.jooq.meta.sybase.SybaseDatabase
               org.jooq.meta.teradata.TeradataDatabase
               org.jooq.meta.vertica.VerticaDatabase

           This value can be used to reverse-engineer generic JDBC DatabaseMetaData (e.g. for MS Access)

               org.jooq.meta.jdbc.JDBCDatabase

           This value can be used to reverse-engineer standard jOOQ-meta XML formats

               org.jooq.meta.xml.XMLDatabase

           This value can be used to reverse-engineer schemas defined by SQL files
           (requires jooq-meta-extensions dependency)

               org.jooq.meta.extensions.ddl.DDLDatabase

           This value can be used to reverse-engineer schemas defined by JPA annotated entities
           (requires jooq-meta-extensions-hibernate dependency)

               org.jooq.meta.extensions.jpa.JPADatabase

           This value can be used to reverse-engineer schemas defined by Liquibase migration files
           (requires jooq-meta-extensions-liquibase dependency)

               org.jooq.meta.extensions.liquibase.LiquibaseDatabase

           You can also provide your own org.jooq.meta.Database implementation
           here, if your database is currently not supported -->
      <name>org.jooq.meta.oracle.OracleDatabase</name>

      <!-- All elements that are generated from your schema (A Java regular expression.
           Use the pipe to separate several expressions) Watch out for
           case-sensitivity. Depending on your database, this might be
           important!

           You can create case-insensitive regular expressions using this syntax: (?i:expr)

           Whitespace is ignored and comments are possible.
           -->
      <includes>.*</includes>

      <!-- All elements that are excluded from your schema (A Java regular expression.
           Use the pipe to separate several expressions). Excludes match before
           includes, i.e. excludes have a higher priority -->
      <excludes>
           UNUSED_TABLE                # This table (unqualified name) should not be generated
         | PREFIX_.*                   # Objects with a given prefix should not be generated
         | SECRET_SCHEMA\.SECRET_TABLE # This table (qualified name) should not be generated
         | SECRET_ROUTINE              # This routine (unqualified name) ...
      </excludes>

      <!-- The schema that is used locally as a source for meta information.
           This could be your development schema or the production schema, etc
           This cannot be combined with the schemata element.

           If left empty, jOOQ will generate all available schemata. See the
           manual's next section to learn how to generate several schemata -->
      <inputSchema>[your database schema / owner / name]</inputSchema>
    </database>

    <!-- Generation flags: See advanced configuration properties -->
    <generate/>

    <target>
      <!-- The destination package of your generated classes (within the
           destination directory)

           jOOQ may append the schema name to this package if generating multiple schemas,
           e.g. org.jooq.your.packagename.schema1
                org.jooq.your.packagename.schema2 -->
      <packageName>org.jooq.your.packagename</packageName>

      <!-- The destination directory of your generated classes -->
      <directory>/path/to/your/dir</directory>
    </target>
  </generator>
</configuration>
```

### 自定义策略

```xml
<name>com.xxx.codegen.CustomJavaGenerator</name>  
<strategy>  
    <name>com.xxx.codegen.CustomGeneratorStrategy</name>  
</strategy>
```

### 生成的一些配置
```xml
<generate>  
    <!-- 是否生成pojo -->
	<pojos>true</pojos> 
	<!-- 是否生成针对单表的DAO -->
	<daos>true</daos>  
	<interfaces>true</interfaces>
	<!-- 是否生成Spring的注解 -->  
	<springAnnotations>true</springAnnotations>  
	<pojosEqualsAndHashCode>true</pojosEqualsAndHashCode>  
	<!-- 是否生成JPA注解 -->
	<jpaAnnotations>true</jpaAnnotations>
	<spatialTypes>false</spatialTypes>
</generate>
```

### 字段类型映射
```xml
<forcedTypes>  
    <forcedType>  
        <name>Integer</name>  
        <includeTypes>(SMALLINT)</includeTypes>  
    </forcedType>  
    <forcedType>  
        <name>Boolean</name>  
        <includeTypes>(BIT)</includeTypes>  
    </forcedType>  
</forcedTypes>
```

### 自定义字段类型
```xml
<customTypes>  
    <customType>  
        <name>Geometry</name>  
        <type>org.locationtech.jts.geom.Geometry</type>  
        <binding>com.xxx.codegen.binding.JTSGeometryBinding</binding>  
    </customType>  
</customTypes>
```

```xml
<forcedType>  
    <name>Geometry</name>  
    <types>(geometry|GEOMETRY)</types>  
</forcedType>
```
### 生成包名及目录设置
```xml
<target>  
    <packageName>  
        com.xxx.dao.jooq  
    </packageName>  
    <directory>  
        ${project.basedir}/src/main/java  
    </directory>  
</target>
```

### 多Schema方式
```xml
 <generator>
    <!-- ... -->
    <database>
      <schemata>
        <schema>
          <inputSchema>schema1</inputSchema>
        </schema>
        <schema>
          <inputSchema>schema2</inputSchema>
        </schema>
        <!-- other schema config ... -->
      </schemata>
    </database>
    <!-- ... -->
</generator>
```

#### 多schema情况下,对不同的schema中的指定表进行生成
```xml
<includes>  
    schema1\.db1 | schema1\.db2
    schema2\.db2 | schema2\.db3
</includes>
```

参考文档:

https://www.jooq.org/doc/latest/manual/code-generation/codegen-configuration/

https://jooq.diamondfsd.com/learn/section-7-multiple-datasource