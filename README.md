# Compact Log

[![Join the chat at https://gitter.im/dodekeract/compact-log](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dodekeract/compact-log)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](http://opensource.org/licenses/MIT)
[![Build Status](https://api.travis-ci.org/dodekeract/compact-log.svg)](https://travis-ci.org/dodekeract/compact-log/)
[![Coverage Status](https://coveralls.io/repos/github/dodekeract/compact-log/badge.svg?branch=master)](https://coveralls.io/github/dodekeract/compact-log?branch=master)
[![Code Climate](https://codeclimate.com/github/dodekeract/compact-log/badges/gpa.svg)](https://codeclimate.com/github/dodekeract/compact-log)
[![NPM Downloads](https://img.shields.io/npm/dm/compact-log.svg)](https://www.npmjs.com/package/compact-log)
[![NPM Dependencies](https://david-dm.org/dodekeract/compact-log.svg)](https://david-dm.org/dodekeract/compact-log)

General purpose JavaScript logger, supports namespaces, colors, compact time and 8 log levels.

## Example
![screenshot](https://github.com/dodekeract/raw/raw/master/compact-log.png)

````javascript
var Log = require('compact-log');
var log = new Log({
	path: __dirname + '/log',
	levelMode: 'smartNoBrackets'
});

log.emergency('emergency');
log.alert('alert');
log.critical('critical');
log.error('error');
log.warning('warning');
log.separator();
log.notice('notice');
log.info('info');
log.debug('debug');
log.separator('Separators can use text.', 'info');
log.info('It\'s able to use %s formats!', 'stuff');
log.separator('emergency separator', 'emergency');
log.debug('You can even dump objects.', {
	test: true,
	woah: 'affirmative'
});
log.de('You can use');
log.dbug('some shorter');
log.debu('variations to log!');
log.warning('This is a really long line, which will probably overflow the width of this console window.');

var ns = log.createNamespace({
	name: 'test'
});

ns.sepa('Even separators can use short functions.');
ns.info('Namespaces, yay!');
ns.se(false, 'alert');

var time = log.createNamespace({
	name: 'compressed time test'
});

var n = 0;
setInterval(function () {
	time.debug(n++);
}, 1000);
````

## Installation
Just type ````npm install compact-log````.
If you want to save it as a dependency in ````package.json```` you should use ````npm install compact-log --save````.

## Initialization
````javascript
	var Log = require('compact-log');
	var log = new Log({/*options*/});
	log.info('Hello world!');
````

## Options
You can pass options when calling ````new Log(options)````. Options is an object which can contain the following attributes.

|                 attribute | default value     | description                                                                                                                                     |
|--------------------------:|:------------------|:------------------------------------------------------------------------------------------------------------------------------------------------|
|                  logLevel | 'debug'           | sets the logLevel for console & file logs                                                                                                       |
|           consoleLogLevel | =logLevel         | overrides the logLevel for consoleLogs only                                                                                                     |
|              fileLogLevel | =logLevel         | overrides the logLevel for fileLogs only                                                                                                        |
|         separatorLogLevel | =7                | sets the default logLevel for separators                                                                                                        |
|            compressedTime | 'day'             | shortens the timestamp of each output and logs a time-update output when the given time period is exceeded (e.g. every day) and a log is issued |
|                 levelMode | 'shortNoBrackets' | allows changing of the level names (e.g. ERROR -> E)                                                                                            |
|                     clear | false             | clears the console when a new log instance is created                                                                                           |
|                      path | false             | sets the log folder                                                                                                                             |
| compressedTimeAsSeparator | true              | allows disabling the separator layout for compressedTime-messages                                                                               |
|                prettyJSON | true              | prints the log file's JSON with tab characters and newlines                                                                                     |
|    alternativeColumnCount | 100               | sets the amount of console columns if process.stdout.columns is not defined                                                                     |

### Accepted values for these options
- **logLevel:** none, emergency, alert, critical, error, warning, notice, info, **debug**, 0-8
- **consoleLogLevel:** none, emergency, alert, critical, error, warning, notice, info, **debug**, 0-8
- **fileLogLevel:** none, emergency, alert, critical, error, warning, notice, info, **debug**, 0-8
- **separatorLogLevel:** none, emergency, alert, critical, error, warning, notice, info, **debug**, 0-8
- **compressedTime:** none, year, month, **day**, hour, minute, second
- **levelMode:** short, smart, full, tiny, **shortNoBrackets**, smartNoBrackets, fullNoBrackets, tinyNoBrackets, numbers, single
- **clear** **false**, true
- **path:** **false** or any path to a (existing or non-existing) folder
- **compressedTimeAsSeparator:** **true**, false
- **prettyJSON:** **true**, false

## Methods
### .emergency(args), .emer, .mrgc, .em
Logs a message with logLevel 1 = 'emergency'.
### .alert(args), .aler, .alrt, .al
Logs a message with logLevel 2 = 'alert'.
### .critical(args), .crit, .crtc, .cr
Logs a message with logLevel 3 = 'critical'.
### .error(args), .erro, .rror, .er
Logs a message with logLevel 4 = 'error'.
### .warning(args), .warn, .wrng, .wa
Logs a message with logLevel 5 = 'warning'.
### .notice(args), .noti, .notc, .no
Logs a message with logLevel 6 = 'notice'.
### .info(args), .in
Logs a message with logLevel 7 = 'info'.
### .debug(args), debu, .dbug, .de
Logs a message with logLevel 8 = 'debug'.
### .separator(text, logLevel), .sepa, .se
Creates a separator consisting of a dashed line (-----). If text is specified it will show this text in the line's center. ````logLevel```` will override the default ````separatorLogLevel````.
### .createNamespace(options)
Creates a namespace. Namespaces will automatically append their name to the log message. Options supports ````name: 'enter name here'```` and ````colors: ['array of colors']````. The supported colors are based on [cli-color](https://www.npmjs.com/package/cli-color).
Example:
````javascript
var ns = log.createNamespace({
	name: 'test',
	colors: ['bgYellowBright', 'black']
});
ns.info('It worked!');
// INFO 12:34:56 test It worked!
````

## Example File Log
This is the log output generated by the example used in the beginning of this document. If you need any other output format for your project - please [file an issue on github](https://github.com/dodekeract/compact-log/issues).

### Usual JSON:
````json
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413798},"level":"emergency","message":"emergency"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413799},"level":"alert","message":"alert"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413799},"level":"critical","message":"critical"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413800},"level":"error","message":"error"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413800},"level":"warning","message":"warning"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413802},"level":"notice","message":"notice"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413803},"level":"info","message":"info"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413803},"level":"debug","message":"debug"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413805},"level":"info","message":"It's able to use stuff formats!"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413806},"level":"debug","message":"You can even dump objects.","dump":[{"test":true,"woah":"affirmative"}]}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413807},"level":"debug","message":"You can use"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413807},"level":"debug","message":"some shorter"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413808},"level":"debug","message":"variations to log!"}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413809},"level":"warning","message":"This is a really long line, which will probably overflow the width of this console window."}
{"time":{"human":"2015-03-03 13:40:13 +01:00","stamp":1425386413812},"level":"info","namespace":"test","message":"Namespaces, yay!"}
{"time":{"human":"2015-03-03 13:40:14 +01:00","stamp":1425386414816},"level":"debug","namespace":"compressed time test","message":"0"}
{"time":{"human":"2015-03-03 13:40:15 +01:00","stamp":1425386415817},"level":"debug","namespace":"compressed time test","message":"1"}
````

### Pretty JSON:
This one is shortened, because it takes up much more space.
````json
{
	"time": {
		"human": "2015-03-03 13:33:43 +01:00",
		"stamp": 1425386023343
	},
	"level": "emergency",
	"message": "emergency"
}
{
	"time": {
		"human": "2015-03-03 13:33:43 +01:00",
		"stamp": 1425386023348
	},
	"level": "debug",
	"message": "You can even dump objects.",
	"dump": [
		{
			"test": true,
			"woah": "affirmative"
		}
	]
}
{
	"time": {
		"human": "2015-03-03 13:33:43 +01:00",
		"stamp": 1425386023350
	},
	"level": "info",
	"namespace": "test",
	"message": "Namespaces, yay!"
}
{
	"time": {
		"human": "2015-03-03 13:33:44 +01:00",
		"stamp": 1425386024337
	},
	"level": "debug",
	"namespace": "compressed time test",
	"message": "0"
}
````
