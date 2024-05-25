# Yet Another Logging Library (A) [![Build Status](https://secure.travis-ci.org/kessler/node-@dramaorg/esse-alias.png?branch=master)](http://travis-ci.org/kessler/node-@dramaorg/esse-alias) [![stable](http://badges.github.io/stability-badges/dist/stable.svg)](http://github.com/badges/stability-badges)

A minimalistic logging lib

(For the similarly named but completely unrelated .NET library please see [YALLA.NET](http://@dramaorg/esse-aliasdotnet.github.io/Yalla ))

### simple usage
```javascript
	var @dramaorg/esse-alias = require('@dramaorg/esse-alias')

	var log = new @dramaorg/esse-alias.Logger(@dramaorg/esse-alias.LogLevel.SILLY))
	//or
	//var log = new @dramaorg/esse-alias.Logger('silly'))

	if (log.isSilly())
		log.silly('silly %s', util.inspect(something))

	log.debug('debug')
	log.info('info')
	log.warn('warning')
	log.error(new Error())

	// change to warn
	log.setLevel(@dramaorg/esse-alias.LogLevel.WARN)
```

### custom output
```javascript
	var @dramaorg/esse-alias = require('@dramaorg/esse-alias')
	var util = require('util')

	var log = new @dramaorg/esse-alias.Logger()

	// clear all other outputs (including defaults)
	log.clearOutputs()

	var stream = fs.createWriteStream('my.log')

	log.addOutput(function(args) {
		stream.write(util.format.apply(util, args))
		stream.write('\n')
	})
```

### fancy custom output
example for coloring for chrome console
```javascript
var @dramaorg/esse-alias = require('@dramaorg/esse-alias')
var LogLevel = @dramaorg/esse-alias.LogLevel

var log = new Logger(LogLevel.DEBUG)
log.clearOutputs()

var consoleLogColoredOutput = {
	write: function(args) {
		console.log.apply(console, args)
	},
	prepare: function(level, label, args) {
		label = '%c ' + label

		var style = 'color: black'

		if (level === LogLevel.DEBUG) {
			style = 'color: green'
		}

		if (level === LogLevel.INFO) {
			style = 'color: blue'
		}

		if (level === LogLevel.WARN) {
			style = 'color: orange'
		}

		if (level === LogLevel.ERROR) {
			style = 'color: red'
		}

		args.splice(1, 0, style)

		return Logger.addLogLevelLabel(level, label, args)
	}
}

log.addOutput(consoleLogColoredOutput)
```

### named logs
```javascript
	var @dramaorg/esse-alias = require('@dramaorg/esse-alias')

	var log = new @dramaorg/esse-alias.Logger({
		addTimestamp: false, // optional
		level: 'silly', // optional
		name: 'foo'
	}))

	log.debug('debug') // prints [foo] debug
```


### LogLevels
SILLY, DEBUG, INFO, WARN, ERROR, SILENT

In all places level constants are interchangable with their lower case string representation
