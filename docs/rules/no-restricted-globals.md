---
title: no-restricted-globals - Rules
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow specific global variables (no-restricted-globals)

# 禁用特定的全局变量 (no-restricted-globals)

Disallowing usage of specific global variables can be useful if you want to allow a set of global
variables by enabling an environment, but still want to disallow some of those.

如果你通过启用一个环境想允许使用一组全局变量，但想禁用其中的一部分，那么该规则会很有用。

For instance, early Internet Explorer versions exposed the current DOM event as a global variable
`event`, but using this variable has been considered as a bad practice for a long time. Restricting
this will make sure this variable isn't used in browser code.

例如，早期的 IE 版本暴露了当前 DOM 事件 `event` 作为一个全局变量，但是使用这个变量长时间内被认为不是一个好的实践。限制它的使用需要确保这个变量没有被用在浏览器端的代码中。

## Rule Details

This rule allows you to specify global variable names that you don't want to use in your application.

该规则允许你指定你不想在你的应用中使用的全局变量的名称。

## Options

This rule takes a list of strings, where each string is a global to be restricted:

该规则包含一个字符串列表，每个字符串都是全局受限的。

```json
{
    "rules": {
        "no-restricted-globals": ["error", "event", "fdescribe"]
    }
}
```

Alternatively, the rule also accepts objects, where the global name and an optional custom message are specified:

另外，该规则也接收一个对象选项，指定全局变量名和可选的自定义消息：

```json
{
    "rules": {
        "no-restricted-globals": [
            "error",
            {
                "name": "event",
                "message": "Use local parameter instead."
            },
            {
                "name": "fdescribe",
                "message": "Do not commit fdescribe. Use describe instead."
            }
        ]
    }
}
```

Examples of **incorrect** code for sample `"event", "fdescribe"` global variable names:

全局变量 `"event", "fdescribe"` 的 **错误** 代码示例：

```js
/*global event, fdescribe*/
/*eslint no-restricted-globals: ["error", "event", "fdescribe"]*/

function onClick() {
    console.log(event);
}

fdescribe("foo", function() {
});
```

Examples of **correct** code for a sample `"event"` global variable name:

全局变量 `"event"` 的 **正确** 代码示例：

```js
/*global event*/
/*eslint no-restricted-globals: ["error", "event"]*/

import event from "event-module";
```

```js
/*global event*/
/*eslint no-restricted-globals: ["error", "event"]*/

var event = 1;
```

Examples of **incorrect** code for a sample `"event"` global variable name, along with a custom error message:

`"event"` 全局变量名和一个自定义的错误消息的 **错误** 代码示例：

```js
/*global event*/
/* eslint no-restricted-globals: ["error", { name: "error", message: "Use local parameter instead." }] */

function onClick() {
    console.log(event);    // Unexpected global variable 'event'. Use local parameter instead.
}
```

## Related Rules

* [no-restricted-properties](no-restricted-properties)
* [no-restricted-syntax](no-restricted-syntax)

## Version

This rule was introduced in ESLint 2.3.0.

该规则在 ESLint 2.3.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-restricted-globals.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-restricted-globals.md)
