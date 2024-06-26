# object-equator

对象属性比较器，旧对象和新对象比较，获取新对象被修改的属性

* 目前支持对象属性基础类型比较，包括String,支持对象嵌套
* 支持集合属性类型属性，Collection,Map
* 如果觉得有用，麻烦点个star，如果有好建议可以邮件或评论
* [ 项目地址](https://github.com/JING-START/object-equator)：<https://github.com/JING-START/object-equator>

<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]

本篇README.md面向开发者

## 目录

- [上手指南](#上手指南)
    - [技术架构](#技术架构)
    - [开发前的配置要求](#开发前的配置要求)
    - [安装步骤](#安装步骤)
- [文件目录说明](#文件目录说明)
- [范例](#范例)
- [版本控制](#版本控制)
- [作者](#作者)
- [鸣谢](#鸣谢)

### 上手指南

###### 技术架构

实现方式：使用java反射机制获取比较对象属性
如果对象属性是基础类型或String并且添加了比较注解，不添加则不比对，例：@EqualsAnnotation(value = "String中文名称1", describe = "String属性描述")，那么就会比较该属性值  
如果是比较自定义对象bean或Collection、Map属性，如果添加了注解，则会递归进该引用对象，找到最低层属性基础类型或String \
注意！属性比较条件：添加注解@EqualsAnnotation，属性名称和注解填的value值要一致

###### 开发前的配置要求

1. 作者jdk开发版本:jdk11

###### 安装步骤

1. 复制源码[equator]目录即可使用，可自定义修改代码
```
https://github.com/JING-START/object-equator.git
```
2. 从github上发布包releases下载jar包
3. pom文件添加依赖
```
   <dependency>
        <groupId>io.github.jing-start</groupId>
        <artifactId>object-equator</artifactId>
        <version>1.0-releases</version>
   </dependency>
```

### 文件目录说明
1. test包下是测试用例MainTest，可以查看

```
pom.xml
README.md
src
    └─main
        ├─java
        │  └─equator
        │          AbstractEquator.java
        │          BaseFieldEquator.java
        │          EqualsAnnotation.java
        │          Equator.java
        │          EquatorFieldInfo.java
        │          EquatorUtil.java
        │          SimpleFieldInfo.java
        └─test
            └─demo
                    ExampleEntityOne.java
                    ExampleEntityThree.java
                    ExampleEntityTwo.java
                    MainTest.java
```

### 范例

* 被比较对象需要添加注解如：
  ``@EqualsAnnotation(value = "Byte中文名称1", describe = "Byte属性描述")``

* 调用工具类方法，传入比较对象example1,example2，返回example2被修改的属性值,具体可以查看运行测试类:MainTest
```
     @Test
    public void testSingleObject() {
        ExampleEntityOne example1 = new ExampleEntityOne();
        example1.setBooleanExample(true);
        example1.setStringExample("6");
        ExampleEntityOne example2 = new ExampleEntityOne();
        example2.setByteExample("1".getBytes(StandardCharsets.UTF_8)[0]);
        example2.setBooleanExample(false);
        example2.setStringExample("7");
        List<EquatorFieldInfo> differentFields = EquatorUtil.getDifferentFields(example1, example2);
        differentFields.forEach(info -> {
            System.out.println("属性名: " + info.getFieldName());
            System.out.println("属性中文名: " + info.getFieldNote());
            System.out.println("属性描述: " + info.getFieldDescribe());
            System.out.println("old属性类型: " + info.getFirstFieldType());
            System.out.println("old属性值: " + info.getFirstVal());
            System.out.println("new属性值: " + info.getSecondVal());
            System.out.println("====================================================");
        });
    }
```
输出
```
属性名: booleanExample
属性中文名: Boolean中文名称1
属性描述: Boolean属性描述
old属性类型: class java.lang.Boolean
old属性值: true
new属性值: false
====================================================
属性名: stringExample
属性中文名: String中文名称1
属性描述: String属性描述
old属性类型: class java.lang.String
old属性值: 6
new属性值: 7
```

### 版本控制

该项目使用Git进行版本管理。您可以在repository参看当前可用版本。

### 作者

* 912176434@qq.com
* zhoujingtong123@foxmail.com
* yezeyue@gamil.com

*您也可以在贡献者名单中参看所有参与该项目的开发者。*

### 版权说明

该项目签署了Apache License Version
2.0授权许可，详情请参阅 [LICENSE](https://github.com/JING-START/equator/blob/main/LICENSE)

### 鸣谢

- [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)
- [Img Shields](https://shields.io)
- [Choose an Open Source License](https://choosealicense.com)
- [GitHub Pages](https://pages.github.com)
- [dadiyang](https://github.com/dadiyang/equator)

<!-- links -->

[your-project-path]:https://github.com/JING-START/equator

[contributors-shield]: https://img.shields.io/github/contributors/JING-START/equator?style=flat-square

[contributors-url]: https://github.com/JING-START/equator/pulse

[forks-shield]: https://img.shields.io/github/forks/JING-START/equator?style=flat-square

[forks-url]: https://github.com/JING-START/equator/forks

[stars-shield]: https://img.shields.io/github/stars/JING-START/equator?style=flat-square

[stars-url]: https://github.com/JING-START/equator/stargazers

[issues-shield]: https://img.shields.io/github/issues/JING-START/equator?style=flat-square

[issues-url]: https://github.com/JING-START/equator/issues

[license-shield]: https://img.shields.io/github/license/JING-START/equator?style=flat-square

[license-url]: https://github.com/JING-START/equator/blob/main/LICENSE




