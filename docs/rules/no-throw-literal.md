---
title: no-throw-literal - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/master/docs/rules/no-throw-literal.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Restrict what can be thrown as an exception (no-throw-literal)

# 限制可以被抛出的异常 (no-throw-literal)

It is considered good practice to only `throw` the `Error` object itself or an object using the `Error` object as base objects for user-defined exceptions.
The fundamental benefit of `Error` objects is that they automatically keep track of where they were built and originated.

仅仅 `抛出`(`throw`) `Error` 对象本身或者用户自定义的以 `Error` 对象为基础的异常，被认为是一个很好的实践。使用 `Error` 对象最基本的好处是它们能自动地追踪到异常产生和起源的地方。

This rule restricts what can be thrown as an exception.  When it was first created, it only prevented literals from being thrown (hence the name), but it has now been expanded to only allow expressions which have a possibility of being an `Error` object.

此规则限制了能被抛出的异常。当初次被创建时，它只是阻止字面量被抛出，但是现在已经被扩展到只允许具有 `Error` 对象能力的表达式。

## Rule Details

This rule is aimed at maintaining consistency when throwing exception by disallowing to throw literals and other expressions which cannot possibly be an `Error` object.

此规则目的在于保持异常抛出的一致性，通过禁止抛出字面量和那些不可能是 `Error` 对象的表达式。

Examples of **incorrect** code for this rule:

**错误** 代码示例：

```js
/*eslint no-throw-literal: "error"*/
/*eslint-env es6*/

throw "error";

throw 0;

throw undefined;

throw null;

var err = new Error();
throw "an " + err;
// err is recast to a string literal

var err = new Error();
throw `${err}`

```

Examples of **correct** code for this rule:

**正确** 代码示例：

```js
/*eslint no-throw-literal: "error"*/

throw new Error();

throw new Error("error");

var e = new Error("error");
throw e;

try {
    throw new Error("error");
} catch (e) {
    throw e;
}
```

## Known Limitations

Due to the limits of static analysis, this rule cannot guarantee that you will only throw `Error` objects.

由于静态分析的局限性，此规则不能保证你只会抛出 `Error` 对象。

Examples of **correct** code for this rule, but which do not throw an `Error` object:

**正确** 代码示例如下，该示例不会抛出 `Error` 对象：

```js
/*eslint no-throw-literal: "error"*/

var err = "error";
throw err;

function foo(bar) {
    console.log(bar);
}
throw foo("error");

throw new String("error");

var foo = {
    bar: "error"
};
throw foo.bar;
```

## Version

This rule was introduced in ESLint 0.15.0.

该规则在 ESLint 0.15.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-throw-literal.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-throw-literal.md)
