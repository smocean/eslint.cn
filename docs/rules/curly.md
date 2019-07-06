---
title: curly - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/master/docs/rules/curly.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Require Following Curly Brace Conventions (curly)

# 要求遵循大括号约定 (curly)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

(fixable) [命令行](../user-guide/command-line-interface#fixing-problems)中的 `--fix` 选项可以自动修复一些该规则报告的问题。

JavaScript allows the omission of curly braces when a block contains only one statement. However, it is considered by many to be best practice to _never_ omit curly braces around blocks, even when they are optional, because it can lead to bugs and reduces code clarity. So the following:

当代码块只有一条语句时，JavaScript 允许省略大括号。然而，很多人认为，在块区域前后时刻保留大括号是一种最佳实践，即使他们是可有可无的，因为省略大括号会导致错误，并且降低代码的清晰度。所以以下模式：

```js
if (foo) foo++;
```

Can be rewritten as:

能被重写为：

```js
if (foo) {
    foo++;
}
```

There are, however, some who prefer to only use braces when there is more than one statement to be executed.

然而，依然有人更乐意在有多条执行语句时才使用大括号。

## Rule Details

This rule is aimed at preventing bugs and increasing code clarity by ensuring that block statements are wrapped in curly braces. It will warn when it encounters blocks that omit curly braces.

此规则目的在于，通过确保代码块使用了大括号包裹以避免bug的发生，并且增加代码的清晰度

## Options

### all

Examples of **incorrect** code for the default `"all"` option:

默认选项 `"all"` 的 **错误** 代码示例：

```js
/*eslint curly: "error"*/

if (foo) foo++;

while (bar)
    baz();

if (foo) {
    baz();
} else qux();
```

Examples of **correct** code for the default `"all"` option:

默认选项 `"all"` 的 **正确** 代码示例：

```js
/*eslint curly: "error"*/

if (foo) {
    foo++;
}

while (bar) {
    baz();
}

if (foo) {
    baz();
} else {
    qux();
}
```

### multi

By default, this rule warns whenever `if`, `else`, `for`, `while`, or `do` are used without block statements as their body. However, you can specify that block statements should be used only when there are multiple statements in the block and warn when there is only one statement in the block.

默认情况下当 `if`、`else`、`for`、`while` 或 `do` 不使用大括号包裹代码时，会给出警告。然而，你可以指定当块中有多条语句时才使用大括号，而当代码块中只有一条语句时只会给出警告。

Examples of **incorrect** code for the `"multi"` option:

选项 `"multi"` 的 **错误** 代码示例：

```js
/*eslint curly: ["error", "multi"]*/

if (foo) {
    foo++;
}

if (foo) bar();
else {
    foo++;
}

while (true) {
    doSomething();
}

for (var i=0; i < items.length; i++) {
    doSomething();
}
```

Examples of **correct** code for the `"multi"` option:

选项 `"multi"` 的 **正确** 代码示例：

```js
/*eslint curly: ["error", "multi"]*/

if (foo) foo++;

else foo();

while (true) {
    doSomething();
    doSomethingElse();
}
```

### multi-line

Alternatively, you can relax the rule to allow brace-less single-line `if`, `else if`, `else`, `for`, `while`, or `do`, while still enforcing the use of curly braces for other instances.

另外，你可以放宽规则，允许在单行中省略大括号，而`if`、`else if`、`else`、`for`、`while` 和 `do`，在其他使用中依然会强制使用大括号。实现如上定制，配置规则如下：

Examples of **incorrect** code for the `"multi-line"` option:

`"multi-line"`选项的 **错误** 代码示例：


```js
/*eslint curly: ["error", "multi-line"]*/

if (foo)
  doSomething();
else
  doSomethingElse();

if (foo) foo(
  bar,
  baz);
```

Examples of **correct** code for the `"multi-line"` option:

选项 `"multi-line"` 的 **正确** 代码示例：

```js
/*eslint curly: ["error", "multi-line"]*/

if (foo) foo++; else doSomething();

if (foo) foo++;
else if (bar) baz()
else doSomething();

do something();
while (foo);

while (foo
  && bar) baz();

if (foo) {
    foo++;
}

if (foo) { foo++; }

while (true) {
    doSomething();
    doSomethingElse();
}
```

### multi-or-nest

You can use another configuration that forces brace-less `if`, `else if`, `else`, `for`, `while`, or `do` if their body contains only one single-line statement. And forces braces in all other cases.

如果 `if`、`else if`、`else`、`for`、`while` 和 `do` 的代码主体中只包含一条语句，你可以使用另外一个配置来强制省略大括号。同时在其他的情况下，强制使用大括号。

Examples of **incorrect** code for the `"multi-or-nest"` option:

选项 `"multi-or-nest"` 的 **错误** 代码示例：

```js
/*eslint curly: ["error", "multi-or-nest"]*/

if (!foo)
    foo = {
        bar: baz,
        qux: foo
    };

while (true)
  if(foo)
      doSomething();
  else
      doSomethingElse();

if (foo) {
    foo++;
}

while (true) {
    doSomething();
}

for (var i = 0; foo; i++) {
    doSomething();
}

if (foo)
    // some comment
    bar();
```

Examples of **correct** code for the `"multi-or-nest"` option:

选项 `"multi-or-nest"` 的 **正确** 代码示例：

```js
/*eslint curly: ["error", "multi-or-nest"]*/

if (!foo) {
    foo = {
        bar: baz,
        qux: foo
    };
}

while (true) {
  if(foo)
      doSomething();
  else
      doSomethingElse();
}

if (foo)
    foo++;

while (true)
    doSomething();

for (var i = 0; foo; i++)
    doSomething();

if (foo) {
    // some comment
    bar();
}
```

### consistent

When using any of the `multi*` options, you can add an option to enforce all bodies of a `if`,
`else if` and `else` chain to be with or without braces.

当在使用任何 `multi*` 选项时，你可以添加一个参数来强制 `if`、`else if` 和 `else` 中所有的代码块使用或者不使用大括号。

Examples of **incorrect** code for the `"multi", "consistent"` options:

选项 `"multi", "consistent"` 的 **错误** 代码示例：

```js
/*eslint curly: ["error", "multi", "consistent"]*/

if (foo) {
    bar();
    baz();
} else
    buz();

if (foo)
    bar();
else if (faa)
    bor();
else {
    other();
    things();
}

if (true)
    foo();
else {
    baz();
}

if (foo) {
    foo++;
}
```

Examples of **correct** code for the `"multi", "consistent"` options:

选项 `"multi", "consistent"` 的 **正确** 代码示例：

```js
/*eslint curly: ["error", "multi", "consistent"]*/

if (foo) {
    bar();
    baz();
} else {
    buz();
}

if (foo) {
    bar();
} else if (faa) {
    bor();
} else {
    other();
    things();
}

if (true)
    foo();
else
    baz();

if (foo)
    foo++;

```

## When Not To Use It

If you have no strict conventions about when to use block statements and when not to, you can safely disable this rule.

如果你没有严格约定何时是否使用块语句，你可以放心的禁用此规则。

## Version

This rule was introduced in ESLint 0.0.2.

该规则在 ESLint 0.0.2 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/curly.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/curly.md)
