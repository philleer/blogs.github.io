# Git commit开发规范学习与总结

### 0.前言

好的提交信息有利于我们对项目的理解、开发和维护，值得花时间了解学习。

- (1) 提高项目的整体规范性
- (2) 历史提交清晰明了，可读性好，方便快速浏览或查找
- (3) 便于跟踪工程历史及Code Reviewing
- (4) 便于直接从提交历史生成变更日志

### 1.概述

被广泛认可并应用的应该是[Angular Git Commit Guidelines](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines)，其规范如下。

一条规范的提交信息包含标题、主体内容和注脚，三者分别用空行隔开。书写格式

```bash
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

**通用规则**

- 提交信息中的每一行都不要超过100个字符。
- 如果本次提交是使用`revert`命令回滚之前的某次提交，提交信息的标题前面应该再加上`revert: `字样。同时在主体内容中应注明`This reverts commmit <hash>.`，这里的hash指的是本次提交对应的历史提交的SHA值。

### 2.标题

我们称第一行的`<type>(<scope>): <subject>`部分为提交信息标题。
一个标题占单独一行，一般要求50个字符以内，包含对更改简明扼要的描述。由更改类型、应用范围和提交主题构成，应用范围有时可省略。

#### 2.1 更改类型

`<type>`部分指出当前提交所提供的改变属于哪种类型。

- `feat`: (feature) 添加新特性
- `fix`: (bug fix) 修复漏洞
- `docs`: (documentation) 仅修改文档，如增删改的提交
- `style`: (formatting, missing semi colons etc) 仅修改排版格式，如缩进、空格/制表符/空行、逗号等不改变代码逻辑的内容的提交
- `refactor`: 没有增加新特性或修复漏洞的代码重构
- `test`: (add missing or correct existing tests) 增加新的或者改正当前测试用例
- `perf`: (improve performance) 提升性能
- `chore`: (maintain) 维护，改变构建流程、增加依赖库等

#### 2.2 应用范围

- `<scope>`部分用于指出本次提交影响或涉及的范围，如`$location, $browser, $compile, $rootScope, ngHref, ngClick, ngView, etc`，可能会是数据层、控制层、视图层等。
- 当没有合适的范围描述方法时可以省略，或者当提交涉及的范围不止一个时也可以用一个星号`*`替代。

#### 2.3 提交主题

`<subject>`部分是对提交更改的简要描述。Angular规范提出以下三个要求。

- (1) 使用祈使句、一般现在时态 (eg:“change” not “changed” nor “changes”)
- (2) 首字母不要大写
- (3) 末尾不要加标点

### 3.主体内容

内容部分用来详细描述本次提交做了哪些更改、为什么进行这些更改、会产生什么结果等的信息。基本原则罗列如下，可以根据实际情况适当调整。

- (1) 和提交主题部分相同，使用祈使句、一般现在时
- (2) 为何进行这个变更，可能是修复漏洞、增加新特性或提升性能、稳定性等
- (3) 与改变之前相比结果会有何变化
- (4) 用于解决什么问题，如何解决，具体描述解决问题的步骤
- (6) 是否存在副作用或潜在风险

### 4.注脚

#### 4.1 突破性进展或不兼容变动

所有的突破性进展或不兼容变动都应该在注脚中明确标注出来，以`BREAKING CHANGE:`开头，后面跟一个空格或者两个空行。剩余的部分用来描述更改内容、理由和迁移说明(the description of the change, justification and migration notes)。

#### 4.2 参考问题

修复与某个问题(issue)相关的漏洞之后，应该把终结的问题在注脚信息中单独一行罗列出来，加上关键词`Closes`作为前缀。

例如终结一个相关问题`Closes #234`或同时终结多个相关问题`Closes #123, #245, #992`。注意问题要附加超链接。

### 5.参考示例

- 示例1

	```bash
	style($location): add couple of missing semi colons
	```

- 示例2

	```bash
	feat(directive): ng:disabled, ng:checked, ng:multiple, ng:readonly, ng:selected

	New directives for proper binding these attributes in older browsers (IE).
	Added coresponding description, live examples and e2e tests.

	Closes #351
	```

- 示例3

	```bash
	feat($browser): onUrlChange event (popstate/hashchange/polling)

	Added new event to $browser:
	- forward popstate event if available
	- forward hashchange event if popstate not available
	- do polling when neither popstate nor hashchange available

	Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
	```

- 示例4

	```bash
	docs(guide): updated fixed docs from Google Docs

	Couple of typos fixed:
	- indentation
	- batchLogbatchLog -> batchLog
	- start periodic checking
	- missing brace
	```

- 示例5

	```bash
	feat($compile): simplify isolate scope bindings

	Changed the isolate scope binding options to:
	  - @attr - attribute binding (including interpolation)
	  - =model - by-directional model binding
	  - &expr - expression execution binding

	This change simplifies the terminology as well as
	number of choices available to the developer. It
	also supports local name aliasing from the parent.

	BREAKING CHANGE: isolate scope bindings definition has changed and
	the inject option for the directive controller injection was removed.

	To migrate the code follow the example below:

	Before:

	scope: {
	  myAttr: 'attribute',
	  myBind: 'bind',
	  myExpression: 'expression',
	  myEval: 'evaluate',
	  myAccessor: 'accessor'
	}

	After:

	scope: {
	  myAttr: '@',
	  myBind: '@',
	  myExpression: '&',
	  // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
	  myAccessor: '=' // in directive's template change myAccessor() to myAccessor
	}

	The removed `inject` wasn't generaly useful for directives so there should be no code using it.
	```
### 参考资料

[1] [您必须知道的 Git 分支开发规范](https://juejin.cn/post/6844903635533594632) https://juejin.cn/post/6844903635533594632

[2] [Git Commit Message Conventions](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#) https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#

[3] [Angular Git Commit Guidelines](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines) https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines

（全文完）

---

> **本文作者**  ：phillee
> **发表日期**  ：2021年12月24日
> **本文链接**  ：[<font color=#483D8B>https://www.cnblogs.com/phillee/p/15353020.html</font>](https://www.cnblogs.com/phillee/p/15353020.html)
> **版权声明**  ：自由转载-非商用-非衍生-保持署名（[<font color=#483D8B>创意共享3.0许可协议</font>](https://creativecommons.org/licenses/by-nc-nd/3.0/deed.zh)/[<font color=#483D8B>CC BY-NC-SA 3.0</font>](https://creativecommons.org/licenses/by-nc-sa/3.0/)）。转载请注明出处！
> 限于本人水平，如果文章和代码有表述不当之处，还请不吝赐教。
