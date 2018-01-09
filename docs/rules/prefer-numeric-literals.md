---
title: prefer-numeric-literals - Rules
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow `parseInt()` in favor of binary, octal, and hexadecimal literals (prefer-numeric-literals)

# 不允许用 `parseInt()` 取代二进制，八进制，和十六进制字符 (prefer-numeric-literals)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fix) can automatically fix some of the problems reported by this rule.

（可修复的）`--fix` [命令行](../user-guide/command-line-interface#fix)选项可自动修复一些该规则反映的问题。

The `parseInt()` function can be used to turn binary, octal, and hexadecimal strings into integers. As binary, octal, and hexadecimal literals are supported in ES6, this rule encourages use of those numeric literals instead of `parseInt()`.

`parseInt()` 函数可用于将二进制，八进制和十六进制的字符串转为整数。由于ES6支持二进制，八进制，和十六进制字符，所以该规则鼓励使用这些数字字符而不是 `parseInt()` 。

```js
0b111110111 === 503;
0o767 === 503;
```

## Rule Details

This rule disallows `parseInt()` if it is called with two arguments: a string and a radix option of 2 (binary), 8 (octal), or 16 (hexadecimal).

该规则不允许调用有两个参数的 `parseInt()` ：一个字符串和一个2（进制），8（进制），或16（进制）的基数选项。

Examples of **incorrect** code for this rule:

**错误**代码示例：

```js
/*eslint prefer-numeric-literals: "error"*/

parseInt("111110111", 2) === 503;
parseInt("767", 8) === 503;
parseInt("1F7", 16) === 255;
```

Examples of **correct** code for this rule:

**正确**代码示例：

```js
/*eslint prefer-numeric-literals: "error"*/
/*eslint-env es6*/

parseInt(1);
parseInt(1, 3);

0b111110111 === 503;
0o767 === 503;
0x1F7 === 503;

a[parseInt](1,2);

parseInt(foo);
parseInt(foo, 2);
```

## When Not To Use It

If you want to allow use of `parseInt()` for binary, octal, or hexadecimal integers. If you are not using ES6 (because binary and octal literals are not supported in ES5 and below).

如果你希望允许使用 `parseInt()` 二进制，八进制，或十六进制整数。如果你不使用 ES6 （因为ES5及以下不支持二进制和八进制字符）。

## Compatibility

* **JSCS**: [requireNumericLiterals](http://jscs.info/rule/requireNumericLiterals)

## Version

This rule was introduced in ESLint 3.5.0.

该规则在 ESLint 3.5.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/prefer-numeric-literals.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/prefer-numeric-literals.md)
