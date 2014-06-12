# ampersand-array-input-view

A view module for intelligently rendering and validating inputs that should produce an array of values. Works well with [ampersand-form-view](ampersandjs/ampersand-form-view).

**still a bit broken, just saving progress**

It does the following:

- Automatically shows/hides error messages based on tests
- Exposes control for adding more input fields.
- Exposes control removing all but required number of input fields.
- Will not show error messages pre-submit or it's never had a valid value. This lets people tab-through a form without triggering a bunch of error message.
- Live-validates to always report if in valid state, but only shows messages when sane to do so.

## install

```
npm install ampersand-input-view
```

## example

```javascript
var InputView = require('ampersand-array-input-view');

var field = new InputView({
    // form input `name`
    name: 'client_name',
    // You can replace the built-in template with your own.
    // just give it an html string. Make sure it has a single "root" element that contains:
    //  - an `<input>` element
    //  - an element with a `role="label"` attribute
    //  - an element with a `role="message-container"` attribute (this we'll show/hide)
    //  - an elememt with a `role="message-text"` attribute (where message text goes for error)
    template: // some HTML string
    // Label name
    label: 'App Name',
    // Optional placeholder attribute
    placeholder: 'My Awesome App',
    // optinal intial value if it has one
    value: ['hello'],
    // optional, this is the that will be 
    // replaced by this view. If you don't
    // give it one, it will create one.
    el: document.getElementByID('field'),
    // whether or not this field is required
    numberRequired: 0, // number of answers needed
    // class to set on input when input is valid
    validClass: 'input-valid', // <- that's the default
    // type value to use for the input tag's type value
    type: 'text',
    // class to set on input when input is valid
    invalidClass: 'input-invalid', // <- that's the default
    // Message to use if error is that it's required
    // but no value was set.
    requiredMessage: 'This field is required.',
    // An array of test functions that each input must pass.
    // They will be called in order with the current input value 
    // and you should write your test to return an error message
    // if it fails and something falsey if it passes.
    // Note that these tests get called with the field view instance as 
    // it's `this` context.
    tests: [
        function (val) {
            if (val.length < 5) return "Must be 5+ characters.";
        }
    ],
    // optional, you can pass in the parent view explicitly
    parent:  someViewInstance 
});

// append it somewhere or use it in side an ampersand-form-view
document.querySelector('form').appendChild(field.el);

```

## credits

Created by [@HenrikJoreteg](http://twitter.com/henrikjoreteg).

## license

MIT

