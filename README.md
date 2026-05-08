# Spring Boot 初始化工程说明

本仓库是一个可用的 **Spring Boot + Web + MyBatis + MySQL** 最小骨架，适合作为新项目的起点。克隆到本地后，请按下列清单替换命名，避免出现包名、模块名与主类不一致的问题。

## 技术栈概要

- Java 8、Maven  
- Spring Boot 2.7.6（`spring-boot-starter-web`）  
- MyBatis Spring Boot Starter、MySQL 驱动  
- Lombok  

## 克隆后需要修改的命名

以下默认占位分别为：**组织 `com.nippy`**、**应用模块名 `demo`**、**启动类 `DemoApplication`**。请统一改为你自己的 `组织/公司`、`项目名`、`启动类名`（可与项目名对应）。

### 1. `pom.xml`

| 位置 | 说明 |
|------|------|
| `<groupId>com.nippy</groupId>` | 改为你的 Maven 组织标识（常用反向域名，如 `com.example`）。 |
| `<artifactId>demo</artifactId>` | 改为 Maven 构件名（通常与仓库/目录名一致）。 |
| `<name>demo</name>` | 改为可读的项目显示名（仅元数据，可与 `artifactId` 相同或更友好）。 |
| `<description>…</description>` | 按需修改项目描述。 |
| `spring-boot-maven-plugin` → `<mainClass>com.nippy.demo.DemoApplication</mainClass>` | 改为新包名下的完整主类名，例如 `com.example.myapp.MyAppApplication`。 |

### 2. Java 源码目录与包名

- 将目录 `src/main/java/com/nippy/demo/` 改为你的包路径，例如 `src/main/java/com/example/myapp/`。
- 将目录 `src/test/java/com/nippy/demo/` 同步改为相同包结构。
- 修改所有 `.java` 文件顶部的 `package` 声明，与目录一致。
- **启动类** `DemoApplication.java`：可按习惯改名为 `XxxApplication.java`，并同步修改类名；同时更新 `pom.xml` 中的 `<mainClass>`。
- **测试类** `DemoApplicationTests.java`：修改 `package` 与类名（若重命名了启动类，测试类名也可一并调整）。

### 3. `src/main/resources/application.yml`

| 配置项 | 说明 |
|--------|------|
| `mybatis.type-aliases-package` | 当前为 `com.nippy.demo.mybatis.entity`，改为实体类所在包（若你尚未建 `mybatis/entity` 目录，可先改成计划使用的包，或创建对应目录后再写 Mapper）。 |
| `mybatis.mapper-locations` | 当前为 `classpath:mappers/*xml`；若你修改了 XML 存放路径，需同步改此处。 |

### 4. 根目录与 Git

- 若需要将项目文件夹从 `demo` 重命名为与 `artifactId` 一致，在文件系统中重命名即可，**无需**改 `pom` 里与目录无关的字段。
- 本模板若曾包含 **`.idea/`**，建议不要提交到模板仓库；新人克隆后应在 IDE 中 **Reimport Maven**，由 IDE 重新生成工程配置。

### 5. 数据库（运行前）

工程依赖 MySQL 与 MyBatis，启动前请在 `application.yml`（或 `application-*.yml`）中补充 **`spring.datasource.*`**（url、username、password 等），否则连接数据库阶段可能失败。端口、数据源等按环境自行拆分 profile 即可。

## 本地构建与运行

```bash
mvn clean package
mvn spring-boot:run
```

打包生成的可执行 JAR 位于 `target/` 目录（名称与 `artifactId` 和版本有关）。

---

**自检建议**：全局搜索 `com.nippy` 与 `demo`，确认业务代码与配置中不再残留旧占位名（注意排除 `pom.xml` 里第三方依赖的 `groupId`，不要误改）。
