# 🈲 开发规范

> 拟定于 2023年1月15日

## ESLint

在推荐的规则基础上

```json
"extends": "next/core-web-vitals"
```

要求常量必须使用`const`

要求使用 `let` 或 `const` 而不是 `var`

要求使用骆驼拼写法

* 组件大驼峰
* 变量小驼峰

在数组开括号后和闭括号前强制换行 [详情可见](http://eslint.cn/docs/rules/array-bracket-newline)

```json
"array-bracket-newline": ["error", {"multiline": true}]
```

要求在数组括号内使用一个或多个空格、或折行

```json
"array-bracket-spacing": ["error", "always"]
```

需要一致地使用数组元素之间的换行符

```json
"array-element-newline": ["error", "consistent"]
```

强制在代码块中开括号前和闭括号后有空格

```json
"block-spacing": ["error", "always"]
```

当最后一个元素或属性与闭括号 `]` 或 `}` 在 *不同的行*时，要求使用拖尾逗号；当在 *同一行*时，禁止使用拖尾逗号。

```json
"comma-dangle": ["error", "always-multiline"]
```

要求使用 `const` 声明那些声明后不再被修改的变量

```json
"prefer-const": "error"
```

要求在模板字符串内使用一个空格

```json
 "template-curly-spacing": ["error", "always"]
```

要求在大括号前后使用空格

```json
"object-curly-spacing": ["error", "always"]
```

要求使用单引号

```json
"quotes": ["error", "single"]
```

要求使用分号结尾

```json
"semi": ["error", "always"]
```

文件不得超过300行

```json
"max-lines": ["error", {"max": 300}]
```

**配置总览**

```json
{
  "extends": "next/core-web-vitals",
  "rules": {
    "semi": [
      "error",
      "always"
    ],
    "quotes": [
      "error",
      "single"
    ],
    "no-extra-parens": [
      "error",
      "all"
    ],
    "block-spacing": [
      "error",
      "always"
    ],
    "max-lines": [
      "error",
      {
        "max": 300
      }
    ],
    "array-bracket-spacing": [
      "error",
      "always"
    ],
    "comma-dangle": [
      "error",
      "always-multiline"
    ],
    "template-curly-spacing": [
      "error",
      "always"
    ],
    "array-element-newline": [
      "error",
      "consistent"
    ],
    "object-curly-spacing": [
      "error",
      "always"
    ],
    "array-bracket-newline": [
      "error",
      {
        "multiline": true
      }
    ]
  },
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  }
}
```

## React 规范

1. 需要有`BFF`处理，一个`BFF`可以对接多个前端服务。后端发生的变化都可以在 `BFF`
   层做一些响应的修改，并增加业务缓存，未来还可以将权限控制放在`BFF`层。

   使用 `NextJs` 与 BFF 结合处理，可以通过以下方式实现：

    1. 在 `NextJs` 中使用 `axios` 库与 `BFF` 进行通信
    2. 在 `NextJs` 中使用 `getServerSideProps`方法在服务器端请求 `BFF` 数据并在页面渲染时使用
    3. 在 `BFF` 中处理路由请求，并将数据返回给 `NextJs` 进行渲染
    4. 您还可以在 `BFF` 中使用更复杂的业务逻辑，如权限验证和数据聚合

   总之，`BFF` 作为 `NextJs` 的后端代理，负责与后端数据库进行交互，并将数据返回给 `NextJs` 进行渲染

![](https://upload-images.jianshu.io/upload_images/3100944-0fd3db877ff651a5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1174/format/webp)

2. 统一使用`scss`编写样式
3. 复杂路径使用`@/*`代表`src/*`
4. 所有组件应该全部采用函数式组件，且使用箭头函数。根标签最好使用和组件相同的名称以便在查看元素时区分。

```js
import React from 'react';

const MyComponent = () => {
	return (
		<div className="MyComponent">

		</div>
	);
};

export default MyComponent;
```

2. 避免过渡封装不必要的组件，满足以下条件可封装：

    * 过于复杂，即将或已经超过300行

    * 在多个地方使用

    * 可能会被插入新的功能

    * 根据传入参数有动态的定制化需求

3. 组件应该尽可能的预留插槽，提高可拓展性

4. 尽量把复杂功能提取出来放在自定义`Hooks`中，提高复用性

## 数据库规范

### 设计规范

1. 字段允许适当冗余，以提高查询性能，但必须考虑数据一致。冗余字段应遵循：

    - 不是频繁修改的字段

    - 不是 `varchar` 超长字段，更不能是 `text` 字段

5. 字段尽量设置为 `NOT NULL`， 为字段提供默认值。 如字符型的默认值为一个空字符值串`’’`。数值型默认值为数值 `0`
   逻辑型的默认值为数值 `0`

6. 每个字段和表必须提供清晰的注释

7. 时间统一格式：`YYYY-MM-DD HH:MM:SS`

8. 更新数据表记录时，必须同时更新记录对应的 `gmt_modified` 字段值为当前时间

### 命名规范

1. 库名与应用名称尽量一致

2. 表达是与否概念的字段，必须使用 `is_xxx` 的方式命名，数据类型是 `unsigned tinyint` ( 1表示是，0表示否)

    * 说明：任何字段如果为非负数，必须是 `unsigned`
    * 正例：表达逻辑删除的字段名 `is_deleted`，1 表示删除，0 表示未删除
2. 表名、字段名必须使用小写字母或数字，禁止出现数字开头，禁止两个下划线中间只出现数字。
    * 说明：MySQL 在 Windows 下不区分大小写，但在 Linux 下默认是区分大小写。
    * 所以：数据库 名、表名、字段名，都不允许出现任何大写字母，避免节外生枝。
        * 正例：`health_user`，`rdc_config`
        * 反例：~~`HealthUser`，`rdcConfig`~~
3. 表名不使用复数名词
    * 说明：表名应该仅仅表示表里面的实体内容，不应该表示实体数量

4. 表必备三字段：`id`,`gmt_create`, `gmt_modified`
    * 说明：其中`id`必为主键，类型为`unsigned bigint`、单表时自增、步长为`1`
    * `gmt_create`, `gmt_modified` 的类型均为 `date_time` 类型
        * 前者现在时表示主动创建，后者过去分词表示被动更新

5. 所有时间字段，都以 `gmt_`开始，后面加上动词的过去式，最后不要加上`time` 单词，
    * 例如 `gmt_create`

## GIT规范

### 分支规划

> 隔离代码，保证代码质量，方便团队协作，并且避免在开发过程中出现代码之间的相互影响

1. 主分支：`master`，当前可用的稳定版本，与线上版本一致

2. 开发分支：每个人创建自己的分支，例如 `develop-xxx`

    * 主要用于每个人自己的开发工作

    * 每个人可以在自己的开发分支上进行自由开发，并等待团队其他成员审核合并

3. 特性分支：每个特性创建一个分支 `feature-xxx` （`xxx` 为特性名称）

    * 特性分支主要用于开发新特性，新特性*有时*需要在一个单独的分支中进行开发, 以便在测试和部署时隔离其他代码
    * 当多个特性需要同时开发时，创建多个特性分支，分别开发，以避免代码之间相互影响
    * 特性分支会在完成后合并到 `develop` 分支，在与团队协商（测试）后合并到 `master` 分支

### Commit 规范

```
<type>(<scope>): <subject>
```

示例

```
// 修改了路由模块的BUG
fix(router):fixed an issue where history was lost and could not be rolled back when jumping to home

// 新增了一个配置
feat(config):add an eslint config
```

**type 取值**

1. **feat**：新功能（feature）
2. **fix**：修补bug
3. **docs**：文档（documentation）
4. **style**： 格式（不影响代码运行的变动）
5. **refactor**：重构（即不是新增功能，也不是修改bug的代码变动）
6. **test**：增加测试
7. ~~**chore**：构建过程或辅助工具的变动~~

**scope 取值**

1. scope用于说明 commit 影响的功能，比如路由、配置、模块名等等。

**subject 取值**

1. subject是 commit 目的的简短描述，不超过50个字符。

2. 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
3. 第一个字母小写
4. 结尾不加句号

## 流程规范

### 正常开发流程

1. 每个人在自己的开发分支上进行开发。
2. 经过队长审核后, 将特性分支合并到 `develop`分支。 
3. 经过队长测试后, 将 `develop`分支合并到 `master`分支。
