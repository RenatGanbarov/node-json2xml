# node-json2xml

## Description

Simple JavaScript Object to XML string converter.

## Installation

Install via [npm](https://www.npmjs.com/package/json2xml), which will download `json2xml` and all of its dependencies.

```bash
npm install json2xml
```

## Simple usage

While the name of the repo is `json2xml`, it is really `pojo2xml`, since you will need to run `JSON.parse` on the JSON data prior to converting.

```js
var fs = require('fs');
var json2xml = require('json2xml');

fs.readFile('data.json', 'utf8', function read (err, data) {
  if (err) console.log(err);
  fs.writeFile('data.xml', json2xml(JSON.parse(data)));
});
```

## Options & Behaviour

```js
// none:
json2xml({ a: 1 });
//<a>1</a>

// empty node:
json2xml({ a: '' });
//<a/>

// add header:
json2xml({ a: 1 }, { header: true });
//<?xml version="1.0" encoding="UTF-8"?><a>1</a>

// add node attributes:
json2xml({ a: 1, attr: { b: 2, c: 3 } }, { attributes_key: 'attr' });
// <a b="2" c="3" >1</a>

// add node attributes version 2:
var json = {
	a: {
		aa: {
			bb: "value_bb" 
			attr: { dd: "value_dd" }
		},
		cc: {
			ff: "value_ff" 
			attr: { ee: "value_ee" }
		},
		attr: { d: value_d, e: value_e }
	}
},{ attributes_key: 'attr' }
json2xml(json, { attributes_key: 'attr' });
//<a d="value_d" e="value_e">
//	<aa dd="value_dd">
//		<bb>value_bb</bb>
//	</aa>
//	<cc ee="value_ee">
//		<ff>value_ff</ff>
//	</cc>
//</a>

// arrays:
json2xml([ { a: 1 }, { b: 2 } ]);
//'<a>1</a><b>2</b>

json2xml({ 'items': [ { item: 1 }, { item: 2 } ] });
//'<items><item>1</item><item>2</item></items>'
```
