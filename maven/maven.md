# Maven

## 基础概念

Maven是一个跨平台的构建工具，主要服务于基于Java平台的项目构建、依赖管理和项目信息管理。

`groupId` , `artifactId` , `version` 这三个元素定义了一个项目的基本坐标。

`groupId` 定义了项目属于哪个组，这个组往往和项目所在的公司存在关联

`artifactId ` 定义了当前Maven项目在组中唯一的ID

`version ` 指定了当前Maven项目的版本

`type` 依赖的类型，对应对应项目坐标定义的 `packaging`

`scope` 依赖的范围

`optional` 标记依赖是否可选

`exclusions` 用来排除传递性依赖

Maven 默认项目主代码位于 `src/main/java` 目录

Maven 默认测试代码位于 `src/test/java` 目录

Maven 默认的编译后的class文件放在 `target/classes` 

依赖范围用来控制依赖与三种classpath（编译classpath、测试classpath、运行classpath）的关系。

依赖范围：`compile` （默认范围）, `test` , `probided` , `runtime` , `system` , `import` 

## 基础配置

< repositories >< /repositories > 远程仓库配置

< servers >< /servers > 远程仓库认证

< distributionManagement >< /distributionManagement > 部署到远程仓库

< mirors >< /mirrors > 镜像配置



## 常用命令

`mvn help:system` 

`mvn archetype:generate`  看用骨架生成Maven项目

`mvn dependency:list` 查看已解析依赖



`mvn clean compile` 

`mvn clean test` 

`mvn clean package` 

`mvn clean install` 

> `clean:clean` 将删除target目录
>
> `resources:resources` 
>
> `compile:compile` 将项目主代码编译至 `target/classes` 目录

`mvn clean deploy` 

```flow
st=>start: Start
op1=>operation: compile
op2=>operation: test
op3=>operation: package
op4=>operation: install
e=>end
st->op1->op2->op3->op4->e
```

## 生命周期

Maven 拥有三套相互独立的生命周期，它们分别是  `clean` ， `default` 和 `site` 。`clean` 生命周期的目的是去清理项目，`default` 生命周期的目的是构建项目，`site` 生命周期的目的是建立项目站点。

### clean生命周期

主要目的：清理项目。

1. `pre-clean` 执行一些清理前需要完成的工作
2. `clean` 清理上一次构建生成的文件
3. `psot-clean` 执行一些清理后需要完成的工作

### default生命周期

定义了真正构建时所需要执行的所有步骤，它是所有生命周期中最核心的部分。

1. `validate` 
2. `initialize` 
3. `generate-sources` 
4. `process-sources` 处理项目主资源文件。一般来说，是对 `src/main/resourcees` 目录的内容进行变量替换等工作后，复制到项目输出的主 `classpath` 目录中
5. `generate-resources` 
6. `process-resources` 
7. `compile` 编译项目主源码。一般来说，是对编译 `src/main/java` 目录下的Java文件至项目输出的主 `classpath` 目录中
8. `process-classes` 
9. `generate-test-sources` 
10. `process-test-sources` 处理项目测试资源文件。一般来说，是对 `src/test/resources` 目录的内容进行变量替换等工作后，复制到项目输出的测试  `classpath` 目录中 
11. `generate-test-resources` 
12. `process-test-resources` 
13. `test-compile` 编译项目中的测试代码。一般来说，是编译 `src/test/java` 目录下的Java文件至项目输出的测试 `classpath` 目录中
14. `process-test-classes` 
15. `test` 使用单元测试框架运行测试，测试代码不会被打包或部署
16. `prepare-package` 
17. `package` 接受编译好的代码，打包成可发布的格式，如 JAR
18. `pre-integrantion-test` 
19. `integrantion-test` 
20. `post-integrantion-test` 
21. `verify` 
22. `install` 将包安装到Maven本地仓库，供本地其他Maven项目使用
23. `deploy` 将最终的包复制到远程仓库，供其他开发人员和Maven项目使用

### site生命周期

1. `pre-site` 执行一些在生成项目站点之前需要完成的工作
2. `site` 生成项目站点文档
3. `post-site` 执行一些在生成项目站点之后需要完成的工作
4. `site-deploy` 将生成的项目站点发布到服务器上