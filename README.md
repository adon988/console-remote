<!--<a href="https://github.com/spumko"><img src="https://raw.github.com/spumko/spumko/master/images/from.png" align="right" /></a>
<img src="https://raw.github.com/spumko/hapi/master/images/hapi.png" />
-->

##Remote JavaScript <a href="http://console.re">Console.Re</a> Connector script for advanced realtime logging and debugging. 

Send log, debug or test information from any webpage, web application or node.js to remote logger. View output results on any device: your tablet, phone or in a separate browser window at http://console.re/project-channel-name.

Connector script extends `console` object adding new methods for sending messages to remote logger with:

<a href="#consolerelog">`console.re.log();`</a> <a href="#consolereinfo">`console.re.info();`</a> <a href="#consoleredebug">`console.re.debug();` <a href="#consolerewarn">`console.re.warn();`</a> <a href="#consolereerror">`console.re.error();`</a> <a href="#consolerecount">`console.re.count();`</a> <a href="#consoleretest">`console.re.test();`</a> <a href="#consolereassert">`console.re.assert();`</a> <a href="#consoleretime">`console.re.time();`</a> <a href="#consoleretimeend">`console.re.timeEnd();`</a> <a href="#consoleretrace">`console.re.trace();`</a> <a href="#consolereclear">`console.re.clear();`</a>

Moreover, using in browsers, log information about DOM elements, CSS properties, track Media Queries and Window size changes with:

<a href="#consoleresize">`console.re.size();`</a> <a href="#consolerecss">`console.re.css();`</a> <a href="#consoleremedia">`console.re.media();`</a>

It simplifies front-end (in browsers) and backend (in node.js) web development and testing. No plugins, no browser's extensions requred, pure JavaScript.

<a href="http://console.re">Console.Re</a> connector (client) script works in **<a href="#supported-platforms">all major browsers</a>** (desktop or mobile) and **node.js** server running on Linux, Mac, Windows.

*Note:* This is a client script, not a server, with this code you can connect and send messages to any **project-channel-name** you want on our public `http://console.re` server, you can see your logs at `http://console.re/project-channel-name`. If you need your own privet server with  support or API customization, please <a href="#public-and-private-servers">read this section</a> and <a href="http://console.re/#contact">contact us</a>.

*Warning:* **Use this for Development environment only. Please DO NOT USE IT ON PRODUCTION WEBSITES AND SERVERS.**


For the latest updates follow [@consolere](https://twitter.com/consolere) on twitter.

# Installation and Use


## Node.Js
1) Install using npm as follows:
```
$ npm install console-remote-client
```

2) In your node apps.js use require to include and connect:

```
var consolere = require('console-remote-client').connect('console.re','80','YOUR-CHANNEL-NAME');
```
3) **[required]** change connect function argument `YOUR-CHANNEL-NAME` to your own `project-channel-name` (any string)

4) add in your code `console.re.log('my first remote log');`

5) open logger in your favorite browser: `http://console.re/project-channel-name`

6) restart your app.js and you should see in logger `[log] my first remote log`

## Browser

#### Install with single `script` tag. 
1) open your template header or HTML file and include `connector.js` **FIRST** thing in `header` tag or **BEFORE** any other `script` tags:

```html
<script src="//console.re/connector.js" data-channel="YOUR-CHANNEL-NAME" id="consolerescript"></script>
```
2) **[required]** change `YOUR-CHANNEL-NAME` in attribute `data-channel` to `project-channel-name` (any string)

3) add in your JavaScript code `console.re.log('my first remote log');`

4) open logger in your favorite browser: `http://console.re/project-channel-name`

5) reload your webpage or app, you should see in logger `[log] my first remote log`


Below an example how to include connector.js in `<header>`:
```html
<!DOCTYPE html>
  <html>
    <header>
      <script src="//console.re/connector.js" data-channel="my-website-channel" id="consolerescript"></script>
      <script src="/js/lib/jquery.js"></script>
      <script src="/js/your-script1.js"></script>
      <script src="/js/your-script2.js"></script>
      <script src="/js/your-script3.js"></script>
    </header>
    ...
```

#### Install with javascript code.

1) include this JavaScript **BEFORE** your code or wrap it with `<script></script>` and place it in `header` **BEFORE** any other `script` tags:

```javascript
  window.consoleRe = {
    channel          : 'YOUR-CHANNEL-NAME' // Case-sensitive! Your project or custom channel name you want to connect: http://console.re/project-channel-name
  };
  // Load the Console.Re API asynchronously
  (function(){if (document.getElementById('consolerescript')) {return;}var f = document.getElementsByTagName('script')[0],s = document.createElement('script');s.id = 'consolerescript';s.src = '//console.re/connector.js';f.parentNode.insertBefore(s,f);}());

```
2) **[required]** change `YOUR-CHANNEL-NAME` in key `channel` to `project-channel-name` (any string)

4) open logger in your favorite browser: `http://console.re/your-own-secret-channel-name`

5) reload your webpage or app, you should see in logger `[log] my first remote log`

## API
### console.re.log() 
Sends `LOG` level message with `string`, `object`, `array`, `number`, `DOM Element` to remote console.
#####`console.re.log(object|array|selector|'string %s',string|'string %d',number[,object, ...]);`
Interpolation allows to insert the value of next argument inside previous string with `%s` or `%d`

````javascript
var s = 'Test';
console.re.log('This is a string %s', s);
[1] Console.Re Logger - [LOG] This is a string 'Test'

var n = 43;
console.re.log('This is a number %d', n);
[2] Console.Re Logger - [LOG] This is a number 43
````

### console.re.info()
Sends `INFO` level message to remote console with optional arguments same as `console.re.log()`.
#####`console.re.info(message);`

### console.re.warn()
Sends `WARN` level message to remote console with optional arguments same as `console.re.log()`.
#####`console.re.warn(message);`

### console.re.debug()
Sends `DEBUG` level message to remote console with optional arguments same as `console.re.log()`.
#####`console.re.debug(message);`

### console.re.error()
Sends `ERROR` level message to remote console with optional arguments same as `console.re.log()`.
#####`console.re.error(message);`

### console.re.size()
Displays size of DOM element(s), `width` and `height` for given `selector(s)` or displays current `Window` size if called with no arguments. Use any `jQuery` selectors if `jQuery` library included in project. *This is browser only API*.
#####`console.re.size([selector],[,selector,...]);`

### console.re.css()
Displays value of specified CSS `properties` in array for given `selector(s)`. Use any `jQuery` selectors if `jQuery` library included in project. *This is browser only API*.
#####`console.re.css(selector,['property','property2', ... 'propertyN']);`

### console.re.media()
Displays value of CSS Media Queries for current `Window` size. An optional `'watch'` argument sets listener to display value of Media Queries on browser's `resize` or device's `orientation` change events. *This is browser only API*.
#####`console.re.media(['watch']);`

### console.re.time()
Creates a new timer under the given `label`, to stop timer and display time result call `console.re.timeEnd(label);` with the same `label`.
#####`console.re.time(label);`

### console.re.timeEnd()
Stops timer and display time result started before with given `label`.
#####`console.re.timeEnd(label);`

### console.re.count()
Displays the number of times count call with given `label` was executed.
#####`console.re.count(label);`

### console.re.test()
Displays result of test for given `expression`, `object`, `string`, `array`, `number`.
#####`console.re.test('expression|string|array|object|number'[,object, ...]);`

Use `quotes` to wrap logic and display original `expression` string along with results:    

````javascript
console.re.test('1!==1', "'this string'", '[1,2,3,4,5,6]');
[1] Console.Re Logger - [TEST] 1!==1 is false,'this string' is "String"‌,[1,2,3,4,5,6,7,8,9,10] is [Array]
````

### console.re.assert()
Tests if a given expression is `true`. Only if not, it will display an error `message`.
#####`console.re.assert(expression[, object, ...],[message])`

### console.re.trace()
Displays stack trace of JavaScript execution at the point where it was called.
#####`console.re.trace();`

### console.re.clear()
Clears remote console logs.
#####`console.re.clear();`


## Usage Examples


Access Console.Re Logger: 
http://console.re/project-channel-name
Usage Examples:
var s = 'Test';
console.re.log('This is a string %s', s);
=> [log] This is a string 'Test'
var n = 43;
console.re.log('This is a number %d', n);
=> [log] This is a number 43
var o = {key1:1,key2:2};
console.re.log('This is an %d', o);
=> [log] This is am {Object}


## Features

- Realtime, effective cross browser development and device independent testing
- Detached remote logging and debuging with extended console API functionality
- View JavaScript logs on any mobile device, tablet or phones (iOS, Android, Windows)
- Easy to read, pretty log output for Objects, Array, JSON, HTML elements, CSS
- Faster Responsive Design development with Media Query logging and tracking
- Watch Media Query changes on browser resize event and device orientation change
- Using [BBcodes] display log information in different styles and colors
- Better logging output with string and number interpolation using `%s` and `%d`
- Connector script is light, framework independed, pure JavaScript solution
- Connector script works in all major browsers (IE6+) can be used to debug desktop and mobile web applications
- Works on server in Node.js running on Linux, Mac, Windows
- Command line interface (CLI) on server allows to send remote logs from OS shell

Enjoy faster web development process!

## Supported Platforms

Console.Re Connector API (client) works on Desktop, Mobile and Server: 

###Desktop browser:
Internet Explorer 6+

Safari 3+

Google Chrome 4+

Firefox 3+

Opera 10+

###Mobile browser: 
iPhone Safari

iPad Safari

Android WebKit

WebOs WebKit

###Server:
Node.js

Shell via Command Line Interface


####Support for IE6-7?

Yes, you can include `connector.js` script and use console.re API in IE6-7 but also, you have to add support for JSON. Just include link to `JSON2.js` file in your HTML `<header>` **BEFORE** console.re `connector.js` scripts:
```html
/* JSON support for old browsers */
<script src="//cdn.jsdelivr.net/json2/0.1/json2.min.js"></script>
<script src="//console.re/connector.js" data-channel="YOUR-CHANNEL-NAME" id="consolerescript"></script>
```
## Command Line (CLI)

Install it globally with npm as follows:
```
$ npm install console-remote-client -g
```

Run with:
```
$ console.re -c YOUR-CHANNEL-NAME log 'sent from command line' 
```
where you need to change `-c` option `YOUR-CHANNEL-NAME` to your `project-channel-name` (any string)

You can edit `./console-remote-client/bin/config.js` and permanently change `YOUR-CHANNEL-NAME` then you can run it witout `-c` option: 

```
$ console.re info 'sent from command line'
```

to see all available options and commands use `--help`:
```
$ console.re --help
```


## Run Tests

```
$ CHANNEL=YOUR-CHANNEL-NAME node tests.js
```
Change `YOUR-CHANNEL-NAME` to `project-channel-name` and run tests

## Public and Private Servers

For moderate use, you can connect and see your logging information on our public server at http://console.re for free. No registration required. Just install connector script and use any string as your channel name. 

All information sent to public server will be open for anyone to see if they know your channel name.

If you need a private and more secure solution. We can offer a dedicated or virtual servers for personal or companies usage. We can provide a  complete solution where you can use your own Remote JavaScript Console server, installed behide your firewall and inside your network.

If you interesting, please contact us with additional information about your organization size and approximate number of users.

In additional, can we provide a custom solution with full support for a large clients. Customize logger or connector API to fit your own unique needs.

## More information

- For the latest updates follow [@consolere](https://twitter.com/consolere) on twitter.
- For more **information, tutorials, and references** on the currently published version.
- Any **issues or questions** (no matter how basic), please open an issue.

## Contact

- website form: http://console.re#contact
- twitter: [@consolere](https://twitter.com/consolere)

## Copyright
Copyright (c) 2013 Sergey Kurdin, AnotherVision.com

Based on http://jsoverson.github.io/rcl 
Copyright (c) 2012 by Jarrod Overson

## License

The MIT License (MIT)

###Warning: Use this for Development environment only. PLEASE MAKE SURE IT REMOVED FROM YOUR PRODUCTION WEBSITES AND SERVERS.
