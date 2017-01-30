---
title: Pretty Printing JavaScript Objects
category: software
layout: post
---

[`JSON.stringify`][1] can pretty-print.  Its arity is three: in addition to the `value` argument, a `replacer` function and `space` value can be passed.

The `replacer` is a function that can be used to modify the `value` as it's converted to a string.  The `space` parameter is either a string or number. You can pass the string to be used as white space (`"  "`), or use a Number to specify how many spaces should be used for indentation.

Pretty-print an object, using two spaces for indentation:

    > var value = { name: 'Ryan', handsome: true };
    undefined
    > JSON.stringify(value, undefined, 2);
    '{\n  "name": "Ryan",\n  "handsome": true\n}'

More details on the `replacer` argument can be found on [Mozilla Developer Network][2].

Or, for easier use, you can create a wrapper:

    > function pp(value) {
        JSON.stringify(value, undefined, 2);
        return value;
      }

[1]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
[2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#The_replacer_parameter
