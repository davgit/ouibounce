# Ouibounce
> Built by [Carl Sednaoui](http://carlsednaoui.com/about?utm_source=github&utm_medium=ouibounce-description&utm_campaign=carl-sednaoui) — Marketing Engineer at [Thinkful](http://www.thinkful.com?utm_source=github&utm_medium=ouibounce-description&utm_campaign=carl-sednaoui), Co-Creator of [MailCharts](http://www.mailcharts.com/?utm_source=github&utm_medium=ouibounce-description&utm_campaign=carl-sednaoui).  



[![tests](http://img.shields.io/travis/carlsednaoui/ouibounce.svg?style=flat)](https://travis-ci.org/carlsednaoui/ouibounce) [![twitter](http://img.shields.io/badge/twitter-@carlsednaoui-blue.svg?style=flat)](http://twitter.com/carlsednaoui)

A small library enabling you to display a modal before a user leaves your website.

![](http://cl.ly/image/2C2p0l3W1M00/ouibounce.gif)

> **Quick note**: [Let me know](https://twitter.com/carlsednaoui) if you end up using Ouibounce. I'd love to hear about your project / see Ouibounce in the wild :)

### The philosophy behind this project

This library helps you increase landing page conversion rates. From my experience, you can expect a lift of 7% to 15% depending on your audience, traffic type (paid or unpaid) and copy.

Talking about copy... __please__ use Ouibounce to __provide value__ to your visitors. With tools like these __it's very easy to create something spammy-looking__.

Not sure what I mean by _provide value_? Here are a few ideas to get your creative juices flowing:

- Free ebook
- Upcoming webinar invite
- Exclusive access to XYZ
- [A full educational course](http://do.thelandingpagecourse.com/)
- [Valuable content](https://training.kalzumeus.com/)

## Demo / Examples

- [Example #1](http://carlsednaoui.github.io/ouibounce/)
- [Example #2](http://colors.carlsednaoui.com/)


## Installation

You have a few options to choose from:

- Download the [minified](build/ouibounce.min.js) or [unminified](build/ouibounce.js) script and include it on your page
- Get Ouibounce from [cdnjs.com](http://cdnjs.com/libraries/ouibounce/)
- Use Bower: `curl http://bower.herokuapp.com/packages/ouibounce`
- Use NPM: `npm install git://github.com/carlsednaoui/ouibounce.git`

_Note_: Ouibounce is wrapped by a [umd wrapper](https://github.com/ForbesLindesay/umd), so if you are using _requirejs/amd_ or _commonjs/browserify_, it will still work fine.

## Usage

1. Create a hidden modal
1. Select the modal with vanilla JavaScript (or jQuery) and call `ouibounce`
1. Optional: Save the function's return value to use the public API, allowing you to `fire` or `disable` Ouibounce on demand

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'));
```

_Example with jQuery:_    
```js 
ouibounce($('#ouibounce-modal')[0]);
```

_Example using the public api:_    
```js
var modal = ouibounce(document.getElementById('ouibounce-modal'));
modal.fire()
```

### Options

Ouibounce offers a few options, such as:

- [Sensitivity](#sensitivity)
- [Aggressive mode](#aggressive-mode)
- [Timer](#set-a-min-time-before-ouibounce-fires)
- [Delay](#delay)
- [Callback](#callback)
- [Cookie expiration](#cookie-expiration)
- [Cookie domain](#cookie-domain)
- [Sitewide cookie](#sitewide-cookie)
- [Chaining options](#chaining-options)

##### Sensitivity
Ouibounce fires when the mouse cursor moves close to (or passes) the top of the viewport. You can define how far the mouse has to be before Ouibounce fires. The higher value, the more sensitive, and the more quickly the event will fire. _Defaults to 20._

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), { sensitivity: 40 });
```

##### Aggressive mode
By default, Ouibounce will only fire once for each visitor. When Ouibounce fires, a cookie is created to ensure a _non obtrusive_ experience.

There are cases, however, when you may want to be more aggressive (as in, you want the modal to be elegible to fire anytime the page is loaded/ reloaded). An example use-case might be on your paid landing pages. If you enable `aggressive`, the modal will fire any time the page is reloaded, for the same user.

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), { aggressive: true });
```

##### Set a min time before Ouibounce fires
By default, Ouibounce won't fire in the first second to prevent false positives, as it's unlikely the user will be able to exit the page within less than a second. If you want to change the amount of time that firing is surpressed for, you can pass in a number of milliseconds to `timer`.

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), { timer: 0 });
```

##### Delay
By default, Ouibounce will show the modal immediately.  You could instead configure it to wait `x` milliseconds before showing the modal.  If the user's mouse re-enters the body before `delay` ms have passed, the modal will not appear.  This can be used to provide a "grace period" for visitors instead of immediately presenting the modal window.

_Example:_

```js
// Wait 100 ms
ouibounce(document.getElementById('ouibounce-modal'), { delay: 100 });
```

##### Callback
You can add a callback, which is a function that will run once Ouibounce has been triggered, by using the `callback` option.

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), { callback: function() { console.log('Ouibounce fired!'); } });
```

##### Cookie expiration
Ouibounce sets a cookie by default to prevent the modal from appearing more than once per user. You can add a cookie expiration (in days) using `cookieExpire` to adjust the time period before the modal will appear again for a user. By default, the cookie will expire at the end of the session, which for most browsers is when the browser is closed entirely.

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), { cookieExpire: 10 });
```

##### Cookie domain
Ouibounce sets a cookie by default to prevent the modal from appearing
more than once per user. You can add a cookie domain using
`cookieDomain` to specify the domain under which the cookie should work.
By default, no extra domain information will be added. If you need a
cookie to work also in your subdomain (like blog.example.com and
example.com), then set a cookieDomain such as .example.com (notice the
dot in front).

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), { cookieDomain:
'.example.com' });
```

##### Sitewide cookie
You can drop sitewide cookies by using passing `sitewide: true`.

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), { sitewide: true });
```

##### Chaining options
The options are just javascript objects, you can therefore combine multiple options.

_Example:_    
```js
ouibounce(document.getElementById('ouibounce-modal'), {
  aggressive: true,
  sitewide: true,
  cookieDomain: '.example.com',
  timer: 0,
  callback: function() { console.log('ouibounce fired!'); }
});
```

### Ouibounce API

If you save the object returned by the `ouibounce` function, you get access to a small public API. Use this API to `fire` or `disable` Ouibounce on demand.

_Example:_    
```js
var modal = ouibounce(document.getElementById('ouibounce-modal'));
modal.fire(); // fire the ouibounce event
modal.disable() // disable ouibounce, it will not fire on page exit
modal.disable({ cookieExpire: 50, sitewide: true }) // disable ouibounce sitewide for 50 days. 
```

##### Disable options
The `disable` function accepts a few options:
- [Cookie expiration](#cookie-expiration)
- [Cookie domain](#cookie-domain)
- [Sitewide cookie](#sitewide-cookie)

### Using Ouibounce with other libraries
If you want to use this library with other plugins — such as [Vex](http://github.hubspot.com/vex/docs/welcome/) — you can call ouibounce with `false`. See [#30](https://github.com/carlsednaoui/ouibounce/issues/30) for discussion.


```js
var _ouibounce = ouibounce(false, {
  callback: function() { console.log('ouibounce fired!'); }
});
```

### Legacy JS engines
If you'd like Ouibounce to work in legacy JS engines (IE8 and below, for example), you'll need to add a shim such as [es5-shim](https://github.com/es-shims/es5-shim).

### WordPress
[Kevin Weber](http://kevinw.de/wbounce) wrote [wBounce](https://wordpress.org/plugins/wbounce/), a WordPress plugin. I personally have __not__ tested it, but you should check it out.

### Miscellaneous

- This library provides no guarantees.
- If you are intersted in contributing, make sure to check out [contributing.md](contributing.md).
- Licensed under [MIT](license.md).
- Special thanks to [Zertosh](https://github.com/zertosh), [Jenius](https://github.com/jenius) and all other [contributors](//github.com/carlsednaoui/ouibounce/graphs/contributors).

[![Analytics](https://ga-beacon.appspot.com/UA-49243488-1/ouibounce/readme)](https://github.com/igrigorik/ga-beacon)
