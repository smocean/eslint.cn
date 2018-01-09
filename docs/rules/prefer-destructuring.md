---
title: prefer-destructuring - Rules
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Prefer destructuring from arrays and objects (prefer-destructuring)

# 优先使用数组和对象解构 (prefer-destructuring)

With JavaScript ES6, a new syntax was added for creating variables from an array index or object property, called [destructuring](#further-reading).  This rule enforces usage of destructuring instead of accessing a property through a member expression.

JavaScript ES6 添加了一个新语法，用于从数组索引或对象属性创建变量，称之为[解构](#further-reading)。此规则强制使用解构而不是通过成员表达式访问属性。

## Rule Details

Examples of **incorrect** code for this rule:

**错误**代码示例：

```javascript
// With `array` enabled
var foo = array[0];

// With `object` enabled
var foo = object.foo;
var foo = object['foo'];
```

Examples of **correct** code for this rule:

**正确**代码示例：

```javascript
// With `array` enabled
var [ foo ] = array;
var foo = array[someIndex];

// With `object` enabled
var { foo } = object;
var foo = object.bar;
```

### Options

This rule takes two sets of configuration objects; the first controls the types that the rule is applied to, and the second controls the way those objects are evaluated.

该规则有两组配置对象；第一组控制该规则的适用类型，第二组控制这些对象的评估方式。

The first has two properties, `array` and `object`, which can be used to turn on or off the destructuring requirement for each of those types independently.  By default, both are `true`.

第一组有两个属性， `array` 和 `object` ，用于独立地开启和关闭每种类型的解构需求。默认情况下，都是 `true` 。

The second has a single property, `enforceForRenamedProperties`, that controls whether or not the `object` destructuring rules are applied in cases where the variable requires the property being access to be renamed.

第二个是一个单独的属性，`enforceForRenamedProperties` ，用于控制 `object` 的解构规则是否适用于访问的属性被变量重命名的情况。

Examples of **incorrect** code when `enforceForRenamedProperties` is enabled:

`enforceForRenamedProperties` 启用时的**错误**代码示例：

```javascript
var foo = object.bar;
```

Examples of **correct** code when `enforceForRenamedProperties` is enabled:

`enforceForRenamedProperties` 启用时的**正确**代码示例：

```javascript
var { bar: foo } = object;
```

An example configuration, with the defaults filled in, looks like this:

一个填写了默认值的配置示例，如下所示：

```json
{
  "rules": {
    "prefer-destructuring": ["error", {
      "array": true,
      "object": true
    }, {
      "enforceForRenamedProperties": false
    }]
  }
}
```

## When Not To Use It

If you want to be able to access array indices or object properties directly, you can either configure the rule to your tastes or disable the rule entirely.

如果你希望能够直接访问数组索引或对象属性，可将该规则配置为你的口味或完全禁用该规则。

Additionally, if you intend to access large array indices directly, like:

另外，如果你打算直接访问大数组的索引，如：

```javascript
var foo = array[100];
```

Then the `array` part of this rule is not recommended, as destructuring does not match this use case very well.

那么该规则 `array` 部分是不推荐的，因为解构无法很好地匹配这个示例。

## Further Reading

If you want to learn more about destructuring, check out the links below:

如果你想更好地了解解构，请查看下面的链接：

- [Destructuring Assignment (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [Destructuring and parameter handling in ECMAScript 6 (2ality blog)](http://www.2ality.com/2015/01/es6-destructuring.html)

## Version

This rule was introduced in ESLint 3.13.0.

该规则在 ESLint 3.13.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/prefer-destructuring.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/prefer-destructuring.md)
