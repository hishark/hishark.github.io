---
title: Room Database
date: 2020-10-15 17:04:10
tags:
- Database
- Android
categories: 
- 学习笔记
authors: 
- hishark777
description: 虽然 Android 的第三方 ORM 框架很多，但是亲儿子 Room 不香吗，来看看 Room 怎么用。
---
## 1. 前言
ORM，Object Relational Mapping，对象关系映射，用于实现面向对象编程语言里不同类型系统的数据之间的转换。

目前有很多优秀的第三方框架比如：

- [GreenDao](https://github.com/greenrobot/greenDAO)
- [Ormlite](https://github.com/j256/ormlite-android)
- [LitePal](https://github.com/guolindev/LitePal)

上面这些也不是不能用，但是每次要用的时候左看看右看看，选数据库都要选个半天，直接用原生的 Room 比较省事啦。



## 2. Room 是什么
Room 在 SQLite 上提供了一个抽象层，以便在充分利用 SQLite 的强大功能的同时，能够流畅地访问数据库。

Room 主要包含三个主要的组件：

1. **[数据库](https://developer.android.com/reference/androidx/room/Database)**：包含数据库持有者，并作为应用已保留的持久关系型数据的底层连接的主要接入点。

    使用 [`@Database`](https://developer.android.com/reference/androidx/room/Database) 注解的类应该满足以下三个条件：

      - 该类是继承 [`RoomDatabase`](https://developer.android.com/reference/androidx/room/RoomDatabase) 的抽象类。

      - 在注解中需要添加与数据库关联的实体列表

      - 需要包含具 0 个参数且返回使用 [`@Dao`](https://developer.android.com/reference/androidx/room/Dao) 注解的类的抽象方法。

  在运行时，可以通过调用 `Room.databaseBuilder()` 或 `Room.inMemoryDatabaseBuilder()` 获取 `Database` 的实例。

2. [**Entity**](https://developer.android.com/training/data-storage/room/defining-data)：实体，表示数据库中的表。

3. **[DAO](https://developer.android.com/training/data-storage/room/accessing-data)**：包含用于访问数据库的方法。

首先，使用 Room 数据库来获取与该数据库相关联的数据访问对象 (DAO)。然后，使用每个 DAO 从数据库中获取实体，再将对这些实体的所有更改保存回数据库中。 最后，使用实体来获取和设置与数据库中的表列相对应的值。

## 3. 使用方法
### 3.1 添加依赖

**Java**

```java
    dependencies {
      def room_version = "2.2.5"

      implementation "androidx.room:room-runtime:$room_version"
      annotationProcessor "androidx.room:room-compiler:$room_version"

      // optional - RxJava support for Room
      implementation "androidx.room:room-rxjava2:$room_version"

      // optional - Guava support for Room, 
      // including Optional and ListenableFuture
      implementation "androidx.room:room-guava:$room_version"

      // optional - Test helpers
      testImplementation "androidx.room:room-testing:$room_version"
    }
```

**Kotlin**

```kotlin
    dependencies {
      def room_version = "2.2.5"

      implementation "androidx.room:room-runtime:$room_version"
      kapt "androidx.room:room-compiler:$room_version"

      // optional - Kotlin Extensions and Coroutines support for Room
      implementation "androidx.room:room-ktx:$room_version"

      // optional - Test helpers
      testImplementation "androidx.room:room-testing:$room_version"
    }
```

### 3.2 创建Entity

在 `Entity` 中，至少需要包含一个主键 `@PrimaryKey`。

**Java**

```java
    @Entity
    public class User {
        @PrimaryKey
        public int uid;

        @ColumnInfo(name = "first_name")
        public String firstName;

        @ColumnInfo(name = "last_name")
        public String lastName;
    }
```

**Kotlin**

```kotlin
    @Entity
    data class User(
        @PrimaryKey val uid: Int,
        @ColumnInfo(name = "first_name") val firstName: String?,
        @ColumnInfo(name = "last_name") val lastName: String?
    )
```

### 3.3 创建DAO

`DAO` 表示数据访问对象，在 `DAO` 中，需要创建一系列用于访问数据库的方法，典型的包括下面的增删改查操作。

**Java**

```java
    @Dao
    public interface UserDao {
        @Query("SELECT * FROM user")
        List<User> getAll();

        @Query("SELECT * FROM user WHERE uid IN (:userIds)")
        List<User> loadAllByIds(int[] userIds);

        @Query("SELECT * FROM user WHERE first_name LIKE :first AND " +
               "last_name LIKE :last LIMIT 1")
        User findByName(String first, String last);

        @Insert
        void insertAll(User... users);

        @Delete
        void delete(User user);

        @Update
        void update(User user);
    }
```

**Kotlin**

```kotlin
    @Dao
    interface UserDao {
        @Query("SELECT * FROM user")
        fun getAll(): List<User>

        @Query("SELECT * FROM user WHERE uid IN (:userIds)")
        fun loadAllByIds(userIds: IntArray): List<User>

        @Query("SELECT * FROM user WHERE first_name LIKE :first AND " +
               "last_name LIKE :last LIMIT 1")
        fun findByName(first: String, last: String): User

        @Insert
        fun insertAll(vararg users: User)

        @Delete
        fun delete(user: User)

        @Update
        fun update(user: User)
    }
    
```

### 3.4 创建数据库

数据库类需要使用 `@Database` 来注解，且在紧跟着的括号中，要添加与该数据库相关联的实体列表，如代码中的 `User.class`。注解中的 `version` 代表版本号。

如果应用在单个进程中运行，在实例化 AppDatabase 对象时应遵循单例设计模式。每个 RoomDatabase 实例的成本相当高，而应用几乎不需要在单个进程中访问多个实例。

**Java**

```java
    @Database(entities = {User.class}, version = 1)
    public abstract class AppDatabase extends RoomDatabase {
        public abstract UserDao userDao();

        public static synchronized AppDatabase getInstance(Context context) {
          if (instance == null) {
              instance = create(context);
          }
          return instance;
        }

        private static AppDatabase create(Context context) {
          return Room.databaseBuilder(getApplicationContext(),
                    AppDatabase.class, "database-name").build();
        }
    }
    
```

**Kotlin**

```kotlin
    @Database(entities = arrayOf(User::class), version = 1)
    abstract class AppDatabase : RoomDatabase() {
        abstract fun userDao(): UserDao
    }

    @Synchronized
    fun getInstance(context: Context): AppDatabase {
        if (instance == null) {
            instance = create(context)
        }
        return instance
    }

    private fun create(context: Context): AppDatabase {
        return Room.databaseBuilder(
            applicationContext,
            AppDatabase::class.java, "database-name"
        ).build()
}
    
```

### 3.5 使用数据库

创建数据库实例之后就可以愉快的增删改查啦。

**Java**

```java
    AppDatabase db;
    db = AppDatabase.getInstance(context);
    // 增
    db.userDao().insertAll(users);
    // 删
    db.userDao().delete(user);
    // 改 
    db.userDao().update(user);
    // 查
    List<User> users = db.userDao().getAll();
```

**Kotlin**

```kotlin
    val db: AppDatabase
    db = AppDatabase.getInstance(context)
    // 增
    db.userDao().insertAll(users)
    // 删
    db.userDao().delete(user)
    // 改 
    db.userDao().update(user)
    // 查
    val users = db.userDao().getAll()
```

## 4. 注意事项

使用过程中碰到了一些坑，之后补充在这里。#TODO

## 5. 参考
- [https://developer.android.com/training/data-storage/room](https://developer.android.com/training/data-storage/room)
- [https://www.jianshu.com/p/cfde3535233d](https://www.jianshu.com/p/cfde3535233d)
