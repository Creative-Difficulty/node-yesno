[![Build Status](https://travis-ci.org/tcql/node-yesno.svg?branch=master)](https://travis-ci.org/tcql/node-yesno)


yesno is a super simple nodejs library for issuing and handling responses to boolean (or rather, binary) questions 

### Installation

Supports Node 8+.

```bash
npm install yesno
```

### Usage

```javascript
import yesno from 'yesno';        // modern es modules approach

// *OR*

const yesno = require('yesno');   // commonjs approach
```

### Examples


##### basic

```javascript
const ok = await yesno({
    question: 'Are you sure you want to continue?'
});
````

If `yesValues` or `noValues` aren't supplied, yesno falls back on accepting `yes`, `y` , `no`, and `n`.

All yesno responses are case insensitive.


##### Custom Yes/No response values

```javascript
const ok = await yesno({
    question: 'Dude, Is this groovy or what?',
    yesValues: [ 'groovy' ],
    noValues: [ 'or what' ]
});

console.log(ok ? 'Tubular.' : 'Aw, why you gotta be like that?');
```

Now the question only responds to `groovy` as yes and `or what` as no.


##### No default value

Sometimes you may want to ensure the user didn't accidentally accept a default. You can disable the default response by passing null as the defaultValue parameter

```javascript
const ok = await yesno({
    question: 'Are you sure you want to 'rm-rf /' ?',
    defaultValue: null
});
```


##### Handling invalid responses

By default, if the user enters a value that isn't recognized as an acceptable response, it will
print out a message like: 

    Invalid response.
    Answer either yes : (yes, y)
    Or no : (no, n)

and re-ask the question. If you want to change this behavior, you can set the invalid handler before asking your question:

```javascript
const ok = await yesno({
    invalid: function ({ question, defaultValue, yesValues, noValues }) {
        process.stdout.write("\n Whoa. That was not a good answer. Well. No more tries for you.");
        process.exit(1);
    }
});
```
