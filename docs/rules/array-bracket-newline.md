---
title: array-bracket-newline - Rules
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# enforce line breaks after opening and before closing array brackets (array-bracket-newline)

# 在数组左括号之后和右括号之前强制换行 (array-bracket-newline)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fix) can automatically fix some of the problems reported by this rule.

(fixable) [命令行](../user-guide/command-line-interface#fix)中的 `--fix` 选项可以自动修复一些该规则报告的问题。

A number of style guides require or disallow line breaks inside of array brackets.

许多样式指南要求或禁止在数组括号内换行。

## Rule Details

This rule enforces line breaks after opening and before closing array brackets.

该规则强制在数组左括号之后和右括号之前换行。

## Options

This rule has either a string option:

该规则有一个字符串选项：

* `"always"` requires line breaks inside braces

* `"always"` 要求在括号之间换行


* `"never"` disallows line breaks inside braces

* `"never"` 禁止在括号之间换行

Or an object option (Requires line breaks if any of properties is satisfied. Otherwise, disallows line breaks):

或一个对象选项（如果满足条件，则要求换行。否则，禁止换行）：

* `"multiline": true` (default) requires line breaks if there are line breaks inside elements or between elements. If this is false, this condition is disabled.

* `"multiline": true` （默认值）如果数组成员内部或者成员之间有换行符，则都要求换行。如过为false，则该条件禁用。
* `"minItems": null` (default) requires line breaks if the number of elements is at least the given integer. If this is 0, this condition will act the same as the option `"always"`. If this is `null` (the default), this condition is disabled.

* `"minItems": null` （默认值）当数组成员的数量大于或等于给定的整数时要求有换行符。如果是0，等同于选项 `"always"` 。如果为 `null` （默认值），该条件禁用。

### always

Examples of **incorrect** code for this rule with the `"always"` option:

选项 `"always"` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "always"]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

Examples of **correct** code for this rule with the `"always"` option:

选项 `"always"` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "always"]*/

var a = [
];
var b = [
    1
];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```

### never

Examples of **incorrect** code for this rule with the `"never"` option:

选项 `"never"` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "never"]*/

var a = [
];
var b = [
    1
];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```

Examples of **correct** code for this rule with the `"never"` option:

选项 `"never"` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "never"]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

### multiline

Examples of **incorrect** code for this rule with the default `{ "multiline": true }` option:

选项 `{ "multiline": true }` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true }]*/

var a = [
];
var b = [
    1
];
var c = [
    1, 2
];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

Examples of **correct** code for this rule with the default `{ "multiline": true }` option:

选项 `{ "multiline": true }` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true }]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```

### minItems

Examples of **incorrect** code for this rule with the `{ "minItems": 2 }` option:

选项 `{ "minItems": 2 }` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "minItems": 2 }]*/

var a = [
];
var b = [
    1
];
var c = [1, 2];
var d = [1,
    2];
var e = [
  function foo() {
    dosomething();
  }
];
```

Examples of **correct** code for this rule with the `{ "minItems": 2 }` option:

选项 `{ "minItems": 2 }` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "minItems": 2 }]*/

var a = [];
var b = [1];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [function foo() {
    dosomething();
}];
```

### multiline and minItems

Examples of **incorrect** code for this rule with the `{ "multiline": true, "minItems": 2 }` options:

选项 `{ "multiline": true, "minItems": 2 }` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true, "minItems": 2 }]*/

var a = [
];
var b = [
    1
];
var c = [1, 2];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

Examples of **correct** code for this rule with the `{ "multiline": true, "minItems": 2 }` options:

选项 `{ "multiline": true, "minItems": 2 }` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true, "minItems": 2 }]*/

var a = [];
var b = [1];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```


## When Not To Use It

If you don't want to enforce line breaks after opening and before closing array brackets, don't enable this rule.

如果你不希望在左括号之后和右括号之前强制换行，不要请用该规则。

## Compatibility

* **JSCS:** [validateNewlineAfterArrayElements](http://jscs.info/rule/validateNewlineAfterArrayElements)

## Related Rules

* [array-bracket-spacing](array-bracket-spacing)

## Version

This rule was introduced in ESLint 4.0.0-alpha.1.

该规则在 ESLint 4.0.0-alpha.1 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/array-bracket-newline.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/array-bracket-newline.md)
