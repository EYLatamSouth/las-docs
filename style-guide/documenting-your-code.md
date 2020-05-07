
<!-- omit in toc -->
# Documenting your code

This is a detailed spec on how developers should be documenting their code. While inline code
comments are very important, this specification will be focusing on docblock structure.

Docblocks are required for all class methods & properties/attributes. The reason we have this spec,
and the reason that actual language standards exist for docblocks, is so that generators will know
how to parse your code & render consumable html documentation.

For this reason, documentation standards follow the existing spec's that are currently community
standards at the time of writing, and we should be following them.

- Official Python Standard: <https://www.python.org/dev/peps/pep-0008/>
- Official JS Standard: <http://usejsdoc.org>
- Official React Standard: <https://github.com/airbnb/javascript/tree/master/react>

There is a lot of overlap in each spec, so this wiki doc will serve as the reference.


<!-- omit in toc -->
## Contents

- [1. Definitions](#1-definitions)
  - [1.1 Docblock](#11-docblock)
  - [1.2 Description](#12-description)
  - [1.3 Tags](#13-tags)
  - [1.4 Docblock section](#14-docblock-section)
- [2. Comprehensive Examples](#2-comprehensive-examples)
  - [2.1 Language JS](#21-language-js)
- [3. General Rules](#3-general-rules)
- [4. Tech Debt](#4-tech-debt)
- [5. Code Examples in Docblocks](#5-code-examples-in-docblocks)
  - [5.1 JS Example](#51-js-example)
- [6. Nested Parameters](#6-nested-parameters)
  - [6.1 JS Nested Parameters](#61-js-nested-parameters)
- [7. Types](#7-types)
  - [7.1 JS Types](#71-js-types)
- [8. Default & Optional Parameters](#8-default--optional-parameters)
- [9. Editor Integration](#9-editor-integration)
  - [9.1 Writing Docblocks in VSCode](#91-writing-docblocks-in-vscode)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 1. Definitions

### 1.1 Docblock

This is a section of documentation which provides information on several aspects of Structural
Elements.

This is what comes first in every docblock. The short description of what a method/variable is. JS
example:

```js
/**
 * This is a summary. It should always be the first thing in a
 * docblock. It should **NEVER** span more than two lines.
 */
```

### 1.2 Description

This is a more detailed explanation than the summary. It is optional, and if included, it should
always come after the summary. JS example:

````js
/**
 * This is a summary. It should always be the first thing in a
 * docblock. It should **NOT** span more than two lines.
 *
 * This is the description. Typically only included when you have
 * more you want to say about the method/variable you're documenting
 * that can't fit in the 2-line summary.
 *
 * Descriptions can be multiple paragraphs, can include *markdown*,
 * headers, code examples `NOTE:`'s, and other things.
 *
 * ### Examples
 *
 * Example of code block in JS:
 * ```
 * var foo = _.map( this.fooBar );
 * ```
 */
````

### 1.3 Tags

The technical term for the @ descriptors you use in docblocks. Common ones we all know are @param &
@return. A @param tag in a docblock are made up of the tag, a type, a variable name, and a tag
description.

Here's a JS example: \* @param {number} input Any number. Where:

- @param is a tag: there are many tags, and they all begin with the @ symbol.
- {number} is a type. It says that the input to this function needs to be a JavaScript "number"
  type. It could also say string, like {string}, {object}, {Date}, or any other JavaScript built-in
  type. And if you defined a custom class, like FooClass, you can use it as a type too by saying
  {FooClass}.
- input is the name of the input variable. It matches what the code says right below it (function
  addOne(input)).
- any number is the description of the input.

### 1.4 Docblock section

Term referring to the Summary, Description, and different groups of tags that comprise the docblock.
Each section should be separated by a line break. JS example:

```js
/**
 * Counter class constructor.
 *
 * @see {@link DialogModal#show} for full list of options.
 * @see {@link https://developer.mozilla.org/en-US/docs/Web/API/Window/alert}
 * @see {@link https://developer.mozilla.org/en-US/docs/Web/API/Window/dialog}
 *
 * @throws {InvalidArgumentException} Optional @throws description
 * @throws {DivideByZero} Argument x must be non-zero.
 * @throws Will throw an error if the argument is null.
 *
 * @param {jQuery} textField - This is a tag description.
 * @param {jQuery} [$counterEl] - This is another tag description.
 * @param {string} [maxGlue] - This is the last `@param` tag description.
 * @return {Counter} The is the `@return` tag description.
 */
```

## 2. Comprehensive Examples

### 2.1 Language JS

````js
/**
 * Show the dialog modal.
 *
 * NOTE: you can call this method directly, but would typically
 * call the `alert()` or `confirm()` aliases directly instead.
 *
 * Show a confirmation modal with custom html template content:
 *
 * ```
 * DialogModal.show( {
 *     onConfirm: this.onAchknowledgeError.bind( this ) );
 *     content: _.template( $( "#error-template" ).html() )( data),
 *     error: true,
 *     title: "error-title",
 *     type: "confirm",
 * } );
 * ```
 *
 * @see {@link https://developer.mozilla.org/en-US/docs/Web/API/Window/alert}
 * @see {@link https://developer.mozilla.org/en-US/docs/Web/API/Window/dialog}
 *
 * @todo Add unit tests.
 * @todo Add notes in readme.
 *
 * @throws {HttpException} If resource creation fails, throws an exception.
 * @throws {CustomException} If resource query fails, throws an exception.
 *
 * @param {string} reqParam - Required parameters shouldn't have [ ] around them
 * @param {object} [options={}] - Options to pass to show
 * @param {function} [options.cancel] - Callback that executes when user clicks cancel button.
 * @param {string|boolean} [options.cancelButton="cancel-button"] - Cancel button message key. Hides button when false.
 * @param {function} [options.confirm] - Callback that executes when user clicks confirm button.
 * @param {string|boolean} [options.confirmButton="confirm-button"] - Confirm button message key.
 * @param {string} [options.content=""] - Text/html displayed in the dialog.
 * @param {boolean} [options.error=false] - When true, add's error class, and drives error styling.
 * @param {string} [options.title="default-alert-title"] - Translation message key for dialog title bar.
 * @param {boolean} [options.type="alert"] - Type of dialog modal it is. Options are "alert" or "confirm".
 * @return {ConfirmModal} Returns a reference to `this` to allow for chaining
 */
show: function( reqParam, options ) {}
````

## 3. General Rules

- Only use spaces in docblocks! DON'T use tabs.
- Don't bother lining up tag names & descriptions of `@param` & `@return` tags. It's hard to
  enforce.
- Use dashes between the field name and description

**Bad:**

```js
/**
 * Counter class constructor.
 *
 * @param  {jQuery}  $textField   This is a tag description.
 * @param  {jQuery}  [$counterEl] This is another tag description.
 * @return {Counter}              The is the `@return` tag description.
 */
```

^ This looks good but can become unweildy and annoying, and most importantly super annoying to
lint/enforce amongst the team.

**Good:**

```js
/**
 * Counter class constructor.
 *
 * @param {jQuery} $textField - This is a tag description.
 * @param {jQuery} [$counterEl] - This is another tag description.
 * @return {Counter} The is the `@return` tag description.
 */
```

- Different docblock "sections" should be separated by a line break.

**Bad:**

```js
/**
 * Alias for show(), with some default options set.
 * NOTE: This is a longer more detailed description block.
 * @see {@link DialogModal#show} for full list of options.
 * @see {@link https://developer.mozilla.org/en-US/docs/Web/API/Window/alert}
 * @param {object|string} options Modal options object. If string, it represents the modal's content.
 * @param {function} [callback] If `options` param is a string, this will be used as the confirm callback.
 * @return {ConfirmModal} Returns a reference to `this` to allow for chaining
 */
```

**Good:**

```js
/**
 * Alias for show(), with some default options set.
 *
 * NOTE: This is a longer more detailed description block.
 *
 * @see {@link DialogModal#show} for full list of options.
 * @see {@link https://developer.mozilla.org/en-US/docs/Web/API/Window/alert}
 *
 * @param {object|string} options - Modal options object. If string, it represents the modal's content.
 * @param {function} [callback] - If `options` param is a string, this will be used as the confirm callback.
 * @return {ConfirmModal} Returns a reference to `this` to allow for chaining.
 */
```

- `@param` and `@return` tags should always be last in the docblock if they exist. All other tags,
  e.g. `@throws`, `@see`, `@author`, `@todo`, etc. should come between the docblock
  summary/description and the `@param`'s. JS Example:

**Bad:**

```js
/**
 * Alias for show(), with some default options set.
 *
 * NOTE: This is a longer more detailed description block.
 *
 * @param {object|string} options Modal options object. If string, it represents the modal's content.
 *
 * @return {ConfirmModal} Returns a reference to `this` to allow for chaining.
 *
 * @todo Add unit tests :).
 *
 * @see {@link DialogModal#show} for full list of options.
 */
```

**Good:**

```js
/**
 * Alias for show(), with some default options set.
 *
 * NOTE: This is a longer more detailed description block.
 *
 * @see {@link DialogModal#show} for full list of options.
 *
 * @todo Add unit tests :).
 *
 * @param {object|string} options - Modal options object. If string, it represents the modal's content.
 * @return {ConfirmModal} Returns a reference to `this` to allow for chaining.
 */
```

- Use @return, not @returns. @return is supported by both languages.

**Bad:**

```js
/**
 * @returns {boolean}
 */
```

**Good:**

```js
/**
 * @return {boolean}
 */
```

- Always include a single space between tag columns, and a dash padded with spaces between var name
  and summary.

**Bad:**

```js
/**
 * @param  {jQuery}   textField    This is a tag description.
 */
```

**Good:**

```js
/**
 * @param {jQuery} textField - This is a tag description.
 */
```

- Always start summaries, descriptions, and tag descriptions with a capital letter & end with a
  period, or some other punctuation (OPTIONAL, but RECOMMENDED). You have to remember, this is meant
  to be consumed in the generated html documentation in the browser, not in code! It should read
  like english to improve usability.

**Bad:**

```js
/**
 * counter class constructor
 *
 * @param {jQuery} textField - this is a tag description
 */
```

**Good:**

```js
/**
 * Counter class constructor.
 *
 * @param {jQuery} textField - This is a tag description.
 */
```

## 4. Tech Debt

Things we've done wrong in the past, that should be changed:

- Stop repeating function name in docblock summaries, it's repetitive and doesn't read well in
  documentation. Generated docs display function names right next to their respective summaries.
- STOP USING TABS. Stop using tabs in docblocks.
- Use markdown where it applies. Both parsers support Markdown, and in turn they also support HTML
  in docblocks, if you need them. Note that JSDoc supports Github Flavored Markdown.
- Writing docblocks only thinking about how they look in code, and not how they'll look in the
  actual parsed documentation. Just cause you added a line break doesn't make it a new sentence.
  Parsers ignore single line returns, so if you want separate paragraphs be sure to add line breaks
  between them. Write full sentences, INCLUDING punctuation!
- We haven't been adding docblocks to most of our JS code.

## 5. Code Examples in Docblocks

It's extremely helpful for reference purposes to include examples in your docblocks. It's important
to note, there's multiple different ways to do this in both PHP & JS, but we'll show you the
recommended & acceptable ways of doing it here.

### 5.1 JS Example

- JSDoc supports Github Flavored Markdown, so it you want to use triple backticks, that is
  acceptable.
- Standard markdown convention is to indent code blocks. That is also acceptable. Be sure to use 4
  spaces if you use this method.
- While the @example tag will work fine, it's suggested you use one of the other 2 methods instead.
  The @example tag is used in PHPDoc as well, but in a different manner, so it can cause confusion
  between languages.

**Good:**

```js
/**
 * Indented, normal Markdown:
 *
 *     var foo = _.map( this.fooBar );
 */
```

**Acceptable:**

````js
/**
 * Example of code block in JS using Github Flavored Markdown:
 *
 * ```
 * var foo = _.map( this.fooBar );
 * ```
 */
````

**Bad:**

```js
/**
 * Indented, normal Markdown. INDENTED CODE BLOCKS NEED A LINE BREAK BEFORE THEM!
 *     var foo = _.map( this.fooBar );
 */
```

**Not Recommended:**

```js
/**
 * @example
 * var foo = _.map( this.fooBar );
 */
```

## 6. Nested Parameters

It's nice knowing that a specific method parameter is an array/object, but what about the
properties/attributes of that parameter? Sometimes it's very helpful to include details about
"nested parameters" when you're passing in an array or object into a method. JS & PHP have very
different ways of handling this.

### 6.1 JS Nested Parameters

JSDoc takes a different approach to parameters with properties. All the properties should be listed
as their own @param's with the parent object prepended in the variable name, i.e.
options.nestedProperty.

See: <http://usejsdoc.org/tags-param.html#parameters-with-properties>

**Example:**

```js
/**
 * Show the dialog modal.
 *
 * @param {object} [options={}] - Modal options.
 * @param {function} [options.onCancel] - Callback that executes when user clicks cancel button.
 * @param {string|boolean} [options.cancelButton="cancel-button"] - Cancel button message key. Hides button when false.
 * @param {function} [options.onConfirm] - Callback that executes when user clicks confirm button.
 * @param {string|boolean} [options.confirmButton="confirm-button"] - Confirm button message key.
 * @param {string} [options.content=""] - Text/html displayed in the dialog.
 * @param {boolean} [options.error=false] - When true, add's error class, and drives error styling.
 * @param {string} [options.title="default-alert-title"] - Translation message key for dialog title bar.
 * @param {boolean} [options.type="alert"] - Type of dialog modal it is. Options are "alert" or "confirm".
 * @return {ConfirmModal} Returns a reference to `this` to allow for chaining
 */
show: function(options) {}
```

## 7. Types

```js
* @param {string} input - Any string.
```

^^ In this example, string refers to the "type". Here are the different types you should be using
for PHP & JS.

### 7.1 JS Types

**See:** <http://usejsdoc.org/tags-type.html>

**NOTE:** It's recommended that you lowercase any primitive types (boolean, null, undefined, number,
string), and capitalize other types.

1. `string`
1. `number`
1. `boolean`
1. `mixed`
1. `null`
1. `undefined`
1. `Array` - It's preferred that you use one of the following, rather than just Array • mixed[] -
   array of mixed types • string[] - array of strings • number[] - array of numbers • array[] -
   array of arrays • object[] - array of objects • MyClass[] - array of type MyClass • etc.
1. object - For object literals, NOT instance objects. If you want to provide more details about the
   object properties, you can in the format: object.<string, number>, which would represent an
   object with string keys and number values. NOTE: If your method takes or returns an instance of a
   specific class, you should specify the class name as the type, e.g. jQuery, Promise, Element,
   Event, etc.

## 8. Default & Optional Parameters

See <http://usejsdoc.org/tags-param.html#optional-parameters-and-default-values>

**JS Example:**

Optional param's have their var names wrapped in square brackets. Defaults get specified following
the variable name and an equals sign.

```js
/**
 * @param {jQuery} textField - This is a REQUIRED parameter.
 * @param {string} bar="" - This param is required, with an empty string default `""`.
 * @param {jQuery} [$counterEl] - This is an OPTIONAL parameter. Denoted by square brackets.
 * @param {number} [max=50] - This param is optional, with a default of `50`.
 * @param {boolean} [shown=false] - This boolean param is optional, with a default of `false`.
 * @param {string} [foo="Foo Bar"] - This param is optional, with a default of `"Foo Bar"`.
 */
```

## 9. Editor Integration

### 9.1 Writing Docblocks in VSCode

Install the Docblockr plugin (<https://github.com/FlyDreame/vscode-docBlocker>) to easy generate
Docblocks.
