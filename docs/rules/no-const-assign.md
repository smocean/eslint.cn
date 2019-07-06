---
title: no-const-assign - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/master/docs/rules/no-const-assign.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow modifying variables that are declared using `const` (no-const-assign)

# 不允许改变用`const`声明的变量 (no-const-assign)

(recommended) The `"extends": "eslint:recommended"` property in a configuration file enables this rule.

(recommended) 配置文件中的 `"extends": "eslint:recommended"` 属性启用了此规则。

We cannot modify variables that are declared using `const` keyword.
It will raise a runtime error.

我们不能修改使用`const`关键字声明的变量。
它会引发一个运行时错误。

Under non ES2015 environment, it might be ignored merely.

非 ES2015 环境下，它只是可能被忽略。

## Rule Details

This rule is aimed to flag modifying variables that are declared using `const` keyword.

该规则旨在标记修改用`const`关键字声明的变量。

Examples of **incorrect** code for this rule:

**错误** 代码示例：


```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
a = 1;
```

```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
a += 1;
```

```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
++a;
```

Examples of **correct** code for this rule:

**正确** 代码示例：


```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
console.log(a);
```

```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

for (const a in [1, 2, 3]) { // `a` is re-defined (not modified) on each loop step.
    console.log(a);
}
```

```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

for (const a of [1, 2, 3]) { // `a` is re-defined (not modified) on each loop step.
    console.log(a);
}
```

## When Not To Use It

If you don't want to be notified about modifying variables that are declared using `const` keyword, you can safely disable this rule.

如果你不想收到有关修改用`const`关键字声明的变量的通知，你可以禁用此规则。

## Version

This rule was introduced in ESLint 1.0.0-rc-1.

该规则在 ESLint 1.0.0-rc-1 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-const-assign.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-const-assign.md)
