---
title: greenDao 3.X 的使用简析  
date: 2017-01-19 16:13:10   
tags: greenDao 
---
**greenDao 3.X 的使用简析**
- 一个对象关系映射（ORM）的框架，能够提供一个接口通过操作对象的方式去操作关系型数据库，它能够让你操作数据库时更简单、更方便。
- greenDAO github地址：https://github.com/greenrobot/greenDAO

**GreenDao 优点：**

- 性能高，号称Android最快的关系型数据库
- 内存占用小
- 库文件比较小，小于100K
- 支持数据库加密 greendao支持SQLCipher进行数据库加密
- 简洁易用的API


**GreenDao 3.2使用方式**
- 第一步：在项目的Build.gradle(project)中添加如下配置

```
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'org.greenrobot:greendao-gradle-plugin:3.2.1'
    }
}
```
- 第二步：在模块中的Build.gradle(app)中添加如下配置

```
apply plugin: 'org.greenrobot.greendao'

android{
    ……
    greendao{
        // 数据库版本号
        schemaVersion 1
        // 设置DaoMaster，DaoSession，Dao包名
        daoPackage 'xxx.xxx.xxx.gen'
        // 设置DaoMaster，DaoSession，Dao目录
        targetGenDir 'src/main/java'
        //设置生成单元测试目录
        // targetGenDirTest
        //设置自动生成单元测试用例
        // generateTests
    }
    ……
}

dependencies {
    compile 'org.greenrobot:greendao:3.2.0'
}
```
- 第四步：写实体类

```
// 实体注解
@Entity(
    // 如果你有超过一个的数据库结构，可以通过这个字段来区分该实体属于哪个结构
    schema = "myschema",

    //  实体活动状体标志位(默认为false) 若设置为true，实体有更新、删除和刷新方法
    active = true,

    // 在数据库中表的名称，默认为实体的类名 
    nameInDb = "NOTE",

    //  定义索引，可以跨越多个列(默认为实体类成员变量的个数) 
    indexes = {
            @Index(value = "name DESC", unique = true)
    },

    // DAO是否应该创建数据库表的标志(默认为true)
    // 如果你有多对一的表，将这个字段设置为false
    // 或者你已经在GreenDAO之外创建了表，也将其置为false
    createInDb = false
)
public class Note {
    @Id //选定一个long/Long类型的字段作为实体的ID，即数据库中的主键。
    private Long id;
    @NotNull
    private long createTime;
    private String content;
    private String title;
    private int weatherPosition;
    private String localtion;

    @Generated   //hash值会自动生成(hash = 346208569) 
    public Note(Long id, long createTime, String content, String title,
            int weatherPosition, String localtion) {
        this.id = id;
        this.createTime = createTime;
        this.content = content;
        this.title = title;
        this.weatherPosition = weatherPosition;
        this.localtion = localtion;
    }

    @Generated
    public Note() {
    }
    
    //make project后变成会自动生成get/set方法
```
> 说明：  
**实体注解**  
@Entity 实体注解  
**基础属性注解**  
@Id 选定一个long/Long类型的字段作为实体的ID，即数据库中的主键。  
@Generated  GreenDao运行所产生的构造函数或者方法，被此标注的代码可以变更或者下次运行时清除  
@Keep 注解的代码段在GreenDao下次运行时保持不变，注解实体类：默认禁止修改此类，注解其他代码段，默认禁止修改注解的代码段。
@Property 让你自定义字段在数据库中的名称，如果为空，GreenDAO将根据驼峰法将其用”_”分割，并全部转为大写，如userName 变为 USER_NAME。  
@NotNull 使字段在数据库中成为非空字段，通常都会将基本类型加上NonNull标志。   
@Transient 使得字段不再持久化。  
**索引注解**  
@Index：使用@Index作为一个属性来创建一个索引，通过name设置索引别名，也可以通过unique给索引添加约束  
@Unique：向数据库列添加了一个唯一的约束    
**关系注解**   
@ToOne：定义与另一个实体（一个实体对象）的关系  
@ToMany：定义与多个实体对象的关系   

- 第五步：封装GreenDao调用方法

```
public class GreenDaoManager {

    private static GreenDaoManager mInstance; //单例
    private DaoMaster mDaoMaster; //以一定的模式管理Dao类的数据库对象
    private DaoSession mDaoSession; //管理制定模式下的所有可用Dao对象
    public GreenDaoManager() {
        if (mInstance == null) {
            DaoMaster.DevOpenHelper devOpenHelper = new
                    DaoMaster.DevOpenHelper(App.getContext(), "myDay-note", null);
            mDaoMaster = new DaoMaster(devOpenHelper.getWritableDatabase());
            mDaoSession = mDaoMaster.newSession();
        }
    }
    public static GreenDaoManager getInstance() {
        if (mInstance == null) {
            synchronized (GreenDaoManager.class) {
                if (mInstance == null) {
                    mInstance = new GreenDaoManager();
                }
            }
        }
        return mInstance;
    }
    public DaoMaster getMaster() {
        return mDaoMaster;
    }
    public DaoSession getSession() {
        return mDaoSession;
    }
    public DaoSession getNewSession() {
        mDaoSession = mDaoMaster.newSession();
        return mDaoSession;
    }
}
```

- 第六步：执行增删改查

```
// 获取dao实例对象
NoteDao noteDao = GreenDaoManager.getInstance().getSession().getNoteDao();
//执行增删改查操作
// 增
Note note = new Note(null, creatTime, noteContent, noteTitle, weatherPosition,location);
noteDao.insert(note);
// 删
noteDao.deleteByKey(noteId);
// 改
noteDao.update(note);
// 查
QueryBuilder<Note> queryBuilder = noteDao.queryBuilder().where(NoteDao.Properties.Id.eq(noteId));
Note note = queryBuilder.unique();

```
以上即为GreenDao的基本使用方法