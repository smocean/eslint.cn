---
title: no-unused-expressions - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/master/docs/rules/no-unused-expressions.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Unused Expressions (no-unused-expressions)

# 禁止未使用过的表达式 (no-unused-expressions)

An unused expression which has no effect on the state of the program indicates a logic error.

对程序状态没有影响的未使用表达式往往是个逻辑错误。

For example, `n + 1;` is not a syntax error, but it might be a typing mistake where a programmer meant an assignment statement `n += 1;` instead. Sometimes, such unused expressions may be eliminated by some build tools in production environment, which possibly breaks application logic.

例如，`n + 1;` 不是语法错误，但它可能是程序员的书写错误，原本是想写赋值语句 `n += 1;`。有时，生产环境中的一些构建工具可能会消除这些未使用的表达式，这可能会破坏应用程序逻辑。

## Rule Details

This rule aims to eliminate unused expressions which have no effect on the state of the program.

此规则旨在消除不使用的表达式，这些表达式对程序的状态没有影响。

This rule does not apply to function calls or constructor calls with the `new` operator, because they could have *side effects* on the state of the program.

此规则不适用于函数调用或带有 `new` 操作符的构造函数调用，因为它们可能对程序的状态产生“副作用”。

```js
var i = 0;
function increment() { i += 1; }
increment(); // return value is unused, but i changed as a side effect

var nThings = 0;
function Thing() { nThings += 1; }
new Thing(); // constructed object is unused, but nThings changed as a side effect
```

This rule does not apply to directives (which are in the form of literal string expressions such as `"use strict";` at the beginning of a script, module, or function).

该规则不适用于指令（比如在脚本（模块或函数）顶部的 `"use strict";`）。

Sequence expressions (those using a comma, such as `a = 1, b = 2`) are always considered unused unless their return value is assigned or used in a condition evaluation, or a function call is made with the sequence expression value.

连续的表达式（使用逗号分隔，比如 `a = 1, b = 2`）总是被认为为被使用过的，除非它们的返回值被赋值给一个变量或被用在条件表达式中或函数调用。

## Options

This rule, in its default state, does not require any arguments. If you would like to enable one or more of the following you may pass an object with the options set as follows:

此规则在默认情况下，不需要任何参数。如果你想要开启一个或者更多的设置你可以通过一个如下所示的选项对象实现：

* `allowShortCircuit` set to `true` will allow you to use short circuit evaluations in your expressions (Default: `false`).
* `allowShortCircuit` 设置为 `true` 将允许你在表达式中使用逻辑短路求值。（默认为 `false`）
* `allowTernary` set to `true` will enable you to use ternary operators in your expressions similarly to short circuit evaluations (Default: `false`).
* `allowTernary` 设置为 `true` 将允许你在表达式中使用类似逻辑短路求值的三元运算符。（默认为 `false`）。
* `allowTaggedTemplates` set to `true` will enable you to use tagged template literals in your expressions (Default: `false`).
* `allowTaggedTemplates` 设置为 `true` 将允许你在表达式中使用带标签的模板字面量 (默认: `false`)。

These options allow unused expressions *only if all* of the code paths either directly change the state (for example, assignment statement) or could have *side effects* (for example, function call).

这些选项只有在所有的代码路径要么直接改变状态（比如，赋值语句）或可以有 *副作用*（例如，函数调用）才允许出现未使用过的表达式。

Examples of **incorrect** code for the default `{ "allowShortCircuit": false, "allowTernary": false }` options:

默认选项 `{ "allowShortCircuit": false, "allowTernary": false }` 的 **错误** 代码示例：

```js
/*eslint no-unused-expressions: "error"*/

0

if(0) 0

{0}

f(0), {}

a && b()

a, b()

c = a, b;

a() && function namedFunctionInExpressionContext () {f();}

(function anIncompleteIIFE () {});

injectGlobal`body{ color: red; }`

```

Note that one or more string expression statements (with or without semi-colons) will only be considered as unused if they are not in the beginning of a script, module, or function (alone and uninterrupted by other statements). Otherwise, they will be treated as part of a "directive prologue", a section potentially usable by JavaScript engines. This includes "strict mode" directives.

注意，一个或多个字符串表达式（无论有无分号）如果不是在脚本、模块或函数（单独的，不被其它语句打断的）顶部都被认为是未使用过的。否则，它们将被视为对 JavaScript 引擎很有用的指令的一部分。包括严格模式指令：

```js
"use strict";
"use asm"
"use stricter";
"use babel"
"any other strings like this in the prologue";
```

Examples of **correct** code for the default `{ "allowShortCircuit": false, "allowTernary": false }` options:

默认选项 `{ "allowShortCircuit": false, "allowTernary": false }` 的 **正确** 代码示例：

```js
/*eslint no-unused-expressions: "error"*/

{} // In this context, this is a block statement, not an object literal

{myLabel: someVar} // In this context, this is a block statement with a label and expression, not an object literal

function namedFunctionDeclaration () {}

(function aGenuineIIFE () {}());

f()

a = 0

new C

delete a.b

void a
```

### allowShortCircuit

Examples of **incorrect** code for the `{ "allowShortCircuit": true }` option:

选项 `{ "allowShortCircuit": true }` 的 **错误** 代码示例：

```js
/*eslint no-unused-expressions: ["error", { "allowShortCircuit": true }]*/

a || b
```

Examples of **correct** code for the `{ "allowShortCircuit": true }` option:

选项 `{ "allowShortCircuit": true }` 的 **正确** 代码示例：

```js
/*eslint no-unused-expressions: ["error", { "allowShortCircuit": true }]*/

a && b()
a() || (b = c)
```

### allowTernary

Examples of **incorrect** code for the `{ "allowTernary": true }` option:

选项 `{ "allowTernary": true }` 的 **错误** 代码示例：

```js
/*eslint no-unused-expressions: ["error", { "allowTernary": true }]*/

a ? b : 0
a ? b : c()
```

Examples of **correct** code for the `{ "allowTernary": true }` option:

选项 `{ "allowTernary": true }` 的 **正确** 代码示例：

```js
/*eslint no-unused-expressions: ["error", { "allowTernary": true }]*/

a ? b() : c()
a ? (b = c) : d()
```

### allowShortCircuit and allowTernary

Examples of **correct** code for the `{ "allowShortCircuit": true, "allowTernary": true }` options:

选项 `{ "allowShortCircuit": true, "allowTernary": true }` 的 **正确** 代码示例：

```js
/*eslint no-unused-expressions: ["error", { "allowShortCircuit": true, "allowTernary": true }]*/

a ? b() || (c = d) : e()
```

### allowTaggedTemplates

Examples of **incorrect** code for the `{ "allowTaggedTemplates": true }` option:

选项 `{ "allowTaggedTemplates": true }` 的 **错误** 代码示例：

```js
/*eslint no-unused-expressions: ["error", { "allowTaggedTemplates": true }]*/

`some untagged template string`;
```

Examples of **correct** code for the `{ "allowTaggedTemplates": true }` option:

选项 `{ "allowTaggedTemplates": true }` 的 **正确** 代码示例：

```js
/*eslint no-unused-expressions: ["error", { "allowTaggedTemplates": true }]*/

tag`some tagged template string`;
```

## Version

This rule was introduced in ESLint 0.1.0.

该规则在 ESLint 0.1.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-unused-expressions.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-unused-expressions.md)