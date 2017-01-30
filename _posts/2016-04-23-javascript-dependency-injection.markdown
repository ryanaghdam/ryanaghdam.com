---
title: Simple IoC Containers in JavaScript
layout: post
category: software
---

Dependency injection and inversion of control can be very easily implemented in
JavaScript applications without the need for any third-party libraries.


First, two example services that adhere to the same contract.  These services
will export `printLetter`, a function that prints a single letter. One variant
is for `development` mode and another is for `production` mode.

```javascript
// services/letter.js
module.exports = {
  printLetter: function () {
    console.log('a');
  }
};

// services/mocks/letter.js
module.exports = {
  printLetter: function () {
    console.log('b');
  }
};
```

Before defining an IoC container, it's best to start with configuration for the
dependencies and work backwards from there.  Each dependency-specific file will
export an object with each dependency as a property.

```javascript
// dependency/development.js
module.exports = {
  letterService: require('../services/mocks/letter')
};

// dependency/production.js
module.exports =  {
  letterService: require('../services/letter')
};
```

Next, an inversion of control container that exports the appropriate letter
printing service depending on the environment.


```javascript
// dependency/index.js

function getEnvironment() {
  if (typeof process.env.NODE_ENV === 'undefined') {
    return 'development';
  }

  return process.env.NODE_ENV;
}

module.exports = require('./' + getEnvironment());
```

Using those dependencies is as easy as including the container:

```javascript
// index.js

var container = require('./dependency');
var letterService = container.letterService;

letterService.printLetter();
```

Running the application in different Node environments sets a different
dependency on the container.

```
$ node index.js
b

$ NODE_ENV=production node index.js
a
```


Full source code is available on GitHub ([ryanaghdam/IoC-poc][1]).  There is
also an example that supports a [default set of dependencies][2] that can be
overwritten by environment-specific dependencies.


[1]: https://github.com/ryanaghdam/IoC-poc/tree/master
[2]: https://github.com/ryanaghdam/IoC-poc/tree/defaults
