# Maven

## 基础概念

Maven是一个跨平台的构建工具，主要服务于基于Java平台的项目构建、依赖管理和项目信息管理。

`groupId` , `artifactId` , `version` 这三个元素定义了一个项目的基本坐标。

`groupId` 定义了项目属于哪个组，这个组往往和项目所在的公司存在关联

`artifactId ` 定义了当前Maven项目在组中唯一的ID

`version ` 指定了当前Maven项目的版本

Maven 默认项目主代码位于 `src/main/java` 目录

Maven 默认测试代码位于 `src/test/java` 目录





`mvn clean install` 

> `clean:clean` 将删除target目录
>
> `resources:resources` 
>
> `compile:compile` 将项目主代码编译至 `target/classes` 目录

`mvn clean compile` 



```flow
st=>start: Start
op1=>operation: compile
op2=>operation: test
op3=>operation: package
op4=>operation: install
e=>end
st->op1->op2->op3->op4->e
```

