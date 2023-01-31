# 第五届字节跳动青训营

> NextJS 实现掘金社区

## 仓库目录

### 前端

1. [掘金社区](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_nextjs)
2. [后台界面](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_nextjs_bff)

### BFF 层

1. [掘金BFF层](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_nextjs_bff)
2. [后台BFF层](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_cms_bff)

### 后端

1. [文章管理](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_post_service)
2. [人员管理](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_person_service)

### 数据库

1. [人员数据](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_database/tree/master/juejin_person)
2. [文章数据](https://github.com/The-fifth-Bytedance-Youth-Camp/juejin_database/tree/master/juejin_post)
3. ~~[页面数据]()~~

## 项目结构

### 前端

使用了BFF层处理数据，使每个页面仅需要一次请求就能拿到所有需要的数据。
去除了冗余字段。使前端项目结构更加清晰。
使前端项目只有页面样式与页面交互的代码，没有数据处理或者获取的代码。

### 后端

拆分了项目所需功能，根据分类建立了多个 `Express` 项目。
组员可以并行开发互不干涉，增加效率，后期维护也更加方便。
在增加或改动某个功能时，减少代码改动。

### 数据库

因为后端根据需要拆分了项目，数据库也进行了分库。
每个项目都有对应的数据库，互不干涉。

![](https://img1.imgtp.com/2023/01/31/qynKx9ha.jpg)

## 代码规范 && 计划书

1. [团队代码规范](https://github.com/The-fifth-Bytedance-Youth-Camp/.github/blob/master/doc/CodeStyle.md)
2. [第一阶段（页面样式）](https://github.com/The-fifth-Bytedance-Youth-Camp/.github/blob/master/doc/FirstStage(PageStyle).md)
3. [第二阶段计划（动态数据）](https://github.com/The-fifth-Bytedance-Youth-Camp/.github/blob/master/doc/SecondStage(Data).md)
4. [项目测试报告](https://github.com/The-fifth-Bytedance-Youth-Camp/.github/blob/master/doc/ProjectTestReport.md)
