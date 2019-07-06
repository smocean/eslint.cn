---
title: arrow-spacing - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/master/docs/rules/arrow-spacing.md
rule_type: layout
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Require space before/after arrow function's arrow (arrow-spacing)

# 要求箭头函数的箭头之前或之后有空格 (arrow-spacing)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

(fixable) [命令行](../user-guide/command-line-interface#fixing-problems)中的 `--fix` 选项可以自动修复一些该规则报告的问题。

This rule normalize style of spacing before/after an arrow function's arrow(`=>`).

该该规则规范化箭头函数的箭头(`=>`)之前或之后的空格风格。

```js
/*eslint-env es6*/

// { "before": true, "after": true }
(a) => {}

// { "before": false, "after": false }
(a)=>{}
```

## Rule Details

This rule takes an object argument with `before` and `after` properties, each with a Boolean value.

该规则有一个对象参数，属性为`before` 和 `after`，对应的值为布尔类型的值。

The default configuration is `{ "before": true, "after": true }`.

默认配置为 `{ "before": true, "after": true }`。

`true` means there should be **one or more spaces** and `false` means **no spaces**.

`true` 意味着应该有 **一个或多个空格**，`false`意味着 **没有空格**。

Examples of **incorrect** code for this rule with the default `{ "before": true, "after": true }` option:

默认选项 `{ "before": true, "after": true }` 的 **错误** 代码示例：

```js
/*eslint arrow-spacing: "error"*/
/*eslint-env es6*/

()=> {};
() =>{};
(a)=> {};
(a) =>{};
a =>a;
a=> a;
()=> {'\n'};
() =>{'\n'};
```

Examples of **correct** code for this rule with the default `{ "before": true, "after": true }` option:

默认选项 `{ "before": true, "after": true }` 的 **正确** 代码示例：

```js
/*eslint arrow-spacing: "error"*/
/*eslint-env es6*/

() => {};
(a) => {};
a => a;
() => {'\n'};
```

Examples of **incorrect** code for this rule with the `{ "before": false, "after": false }` option:

选项 `{ "before": false, "after": false }` 的 **错误** 代码示例：

```js
/*eslint arrow-spacing: ["error", { "before": false, "after": false }]*/
/*eslint-env es6*/

() =>{};
(a) => {};
()=> {'\n'};
```

Examples of **correct** code for this rule with the `{ "before": false, "after": false }` option:

选项 `{ "before": false, "after": false }` 的 **正确** 代码示例：

```js
/*eslint arrow-spacing: ["error", { "before": false, "after": false }]*/
/*eslint-env es6*/

()=>{};
(a)=>{};
()=>{'\n'};
```

Examples of **incorrect** code for this rule with the `{ "before": false, "after": true }` option:

选项 `{ "before": false, "after": true }` 的 **错误** 代码示例：

```js
/*eslint arrow-spacing: ["error", { "before": false, "after": true }]*/
/*eslint-env es6*/

() =>{};
(a) => {};
()=>{'\n'};
```

Examples of **correct** code for this rule with the `{ "before": false, "after": true }` option:

选项 `{ "before": false, "after": true }` 的 **正确** 代码示例：

```js
/*eslint arrow-spacing: ["error", { "before": false, "after": true }]*/
/*eslint-env es6*/

()=> {};
(a)=> {};
()=> {'\n'};
```

## Version

This rule was introduced in ESLint 1.0.0-rc-1.

该规则在 ESLint 1.0.0-rc-1 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/arrow-spacing.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/arrow-spacing.md)
