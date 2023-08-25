现有的ORM框架：

> MyBatis

MyBatis 是apach 的一个开源项目iBatis。2010年被Google接管，改名为MyBatis。着力于POJO与sql之间的映射关系，可以进行更为细致的SQL编写操作，市场占有率高。

> Hibernate

一个开放源码的对象关系映射框架，它对JDBC进行了非常轻量级的对象封装，使得java程序员可以随心所欲的使用对象编程来操作数据库。对象有自己的生命周期，有自己的HQL查询语言，数据库移植性好。

> Spring Data JPA

在Hibernate的基础上基于JPA规范的再次封装，引用JPQL(java persistence query language)查询语言，属于Spring整体生态体系的一部分。

> OpenJPA

> QueryDSL



**Java Persistence API**

JPA 是 JDK 5.0 新增的协议，通过相关持久层注解（@Entity 里面的各种注解）来描述对象和关系型数据里面的表映射关系，并将 Java 项目运行期的实体对象，通过一种Session持久化到数据库中。

- 一套 API 标准定义了一套接口，在 javax.persistence 的包下面，用来操作实体对象，执行 CRUD 操作，而实现的框架（Hibernate）替代我们完成所有的事情，让开发者从烦琐的 JDBC 和 SQL 代码中解脱出来，更加聚焦自己的业务代码，并且使架构师架构出来的代码更加可控。
- 定义了一套基于对象的 SQL：Java Persistence Query Language（JPQL），像 Hibernate 一样，我们通过写面向对象（JPQL）而非面向数据库的查询语言（SQL）查询数据，避免了程序与数据库 SQL 语句耦合严重，比较适合跨数据源的场景（一会儿 MySQL，一会儿 Oracle 等）。
- ORM（Object/Relational Metadata）对象注解映射关系，JPA 直接通过注解的方式来表示 Java 的实体对象及元数据对象和数据表之间的映射关系，框架将实体对象与 Session 进行关联，通过操作 Session 中不通实体的状态，从而实现数据库的操作，并实现持久化到数据库表中的操作，与 DB 实现同步。
 ![未命名文件 (1)](G:/typora_img/%E6%9C%AA%E5%91%BD%E5%90%8D%E6%96%87%E4%BB%B6%20(1).png)

**Defining Query Method(DQM)**

**@Query**

example one:

```java
public interface UserRepository extends JpaRepository<User, Long>{
    @Query("select u from User u where u.emailAdress = ?1")
    User findByEmailAddress(String emailAdress);
}
```

example two:

```java
public interface UserRepository extends JpaRepository<User, Long>{
    @Query("select u from User u where u.firstname = %?1")
    User findByFirstnameEndsWith(String firstname);
}
```

example three:(使用原始的sql)

```java
public interface UserRepository extends JpaRepository<User, Long>{    @Query(value = "select * from User where email_address = ?1",nativeQuery = true)    User findByEmailAddress(String emailAdress);}
```

**JPA注解**

> Entity

**@Entity** 用于定义对象将会成为被 JPA 管理的实体，必填，将字段映射到指定的数据库表中，使用起来很简单，直接用在实体类上面即可

> Table

**@Table** 用于指定数据库的表名，表示此实体对应的数据库里面的表名，非必填，默认表名和 entity 名字一样。

> Access

**@Access** 用于指定 entity 里面的注解是写在字段上面，还是 get/set 方法上面生效，非必填。在默认不填写的情况下，当实体里面的第一个注解出现在字段上或者 get/set 方法上面，就以第一次出现的方式为准.

> Id

**@Id** 定义属性为数据库的主键，一个实体里面必须有一个主键，但不一定是这个注解，可以和 @GeneratedValue 配合使用或成对出现。

> GeneratedValue

主键生成策略

其中GenerationType一共有以下四个值：

- table：通过表产生主键，框架借由表模拟序列产生主键，使用该策略可以使应用更易于数据库移植。
- sequence：通过序列产生主键，通过@SequenceGenerator注解指定序列名，Mysql不支持这种方式。
- identity：采用数据库ID自增长，一般用于mysql。
- auto（默认值）

> Enumerated

**@Enumerated** 这个注解很好用，因为它对 enum 提供了下标和 name 两种方式，用法直接映射在 enum 枚举类型的字段上。请看下面源码

> Basic

**@Basic** 表示属性是到数据库表的字段的映射。如果实体的字段上没有任何注解，默认即为 @Basic。也就是说默认所有的字段肯定是和数据库进行映射的，并且默认为 Eager 类型。

> Transient

**@Transient** 表示该属性并非一个到数据库表的字段的映射，表示非持久化属性。JPA 映射数据库的时候忽略它，与 @Basic 有相反的作用。也就是每个字段上面 @Transient 和 @Basic 必须二选一，而什么都不指定的话，默认是 @Basic。

> Column

**@Column** 定义该属性对应数据库中的列名

> Temporal

**@Temporal** 用来设置 Date 类型的属性映射到对应精度的字段

TemporalType:

- DATE
- TIME
- TIMESTAMP

>  IdClass

联合主键

> Embeddedld

联合主键



**实体之间的继承关系**

> 纯粹的继承，和表没关系，对象之间的字段共享。利用注解 @MappedSuperclass，协议规定父类不能是 @Entity。

> 单表多态问题，同一张 Table，表示了不同的对象，通过一个字段来进行区分。利用`@Inheritance(strategy = InheritanceType.SINGLE_TABLE)`注解完成，只有父类有 @Table

> 多表多态，每一个子类一张表，父类的表拥有所有公用字段。通过`@Inheritance(strategy = InheritanceType.JOINED)`注解完成，父类和子类都是表，有公用的字段在父表里面

> Object 的继承，数据库里面每一张表是分开的，相互独立不受影响。通过`@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)`注解完成，父类（可以是一张表，也可以不是）和子类都是表，相互之间没有关系。



**实体之间的关系**

> OneToOne

@OneToOne 一般表示对象之间一对一的关联关系，它可以放在 field 上面，也可以放在 get/set 方法上面。其中 JPA 协议有规定，如果是配置双向关联，维护关联关系的是拥有外键的一方，而另一方必须配置 mappedBy；如果是单项关联，直接配置在拥有外键的一方即可。

`CascadeType `级联操作

`orphanRemoval`是否应用级联删除

> JoinCloumns & JoinColumn

这两个注解是集合关系，他们可以同时使用，@JoinColumn 表示单字段，@JoinCloumns 表示多个 @JoinColumn。

> @ManyToOne& @OneToMany

@ManyToOne 代表多对一的关联关系，而 @OneToMany 代表一对多，一般两个成对使用表示双向关联关系。而 JPA 协议中也是明确规定：维护关联关系的是拥有外键的一方，而另一方必须配置 mappedBy。

> @ManyToMany

@ManyToMany 代表多对多的关联关系，这种关联关系任何一方都可以维护关联关系。

