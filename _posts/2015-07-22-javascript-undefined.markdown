---
title: Checking for undefined in JavaScript
layout: post
category: software
---

JavaScript has many quirks, some of which can be found when checking to see if a value is undefined.

In cases where the value is *guaranteed* to be declared, it is possible to use triple-equals.

    > var x;
    undefined
    > x === undefined;
    true

However, if the value is *not* declared, an error will be thrown.

    > y === undefined;
    ReferenceError: y is not defined
        at repl:1:1
        at REPLServer.defaultEval (repl.js:132:27)
        at bound (domain.js:254:14)
        at REPLServer.runBound [as eval] (domain.js:267:12)
        at REPLServer.<anonymous> (repl.js:279:12)
        at REPLServer.emit (events.js:107:17)
        at REPLServer.Interface._onLine (readline.js:214:10)
        at REPLServer.Interface._line (readline.js:553:8)
        at REPLServer.Interface._ttyWrite (readline.js:830:14)
        at ReadStream.onkeypress (readline.js:109:10)

In this case, it's necessary to use `typeof` to determine if the value is undefined.

    > z === undefined;
    ReferenceError: z is not defined
        at repl:1:1
        at REPLServer.defaultEval (repl.js:132:27)
        at bound (domain.js:254:14)
        at REPLServer.runBound [as eval] (domain.js:267:12)
        at REPLServer.<anonymous> (repl.js:279:12)
        at REPLServer.emit (events.js:107:17)
        at REPLServer.Interface._onLine (readline.js:214:10)
        at REPLServer.Interface._line (readline.js:553:8)
        at REPLServer.Interface._ttyWrite (readline.js:830:14)
        at ReadStream.onkeypress (readline.js:109:10)
    > typeof z === 'undefined';
    true
