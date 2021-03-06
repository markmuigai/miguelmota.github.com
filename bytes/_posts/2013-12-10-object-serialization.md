---
layout: byte
title: How to serialize an object in JavaScript
category: bytes
tags: [JavaScript]
description: Serialize an object in Javascript.
---
Serialize an object in JavaScript.

```javascript
function serialize(obj, prefix) {
  var s = function(obj, prefix) {
    var str = [];
    for(var p in obj) {
      var k = prefix ? prefix + '[' + p + ']' : p, v = obj[p];
      if (v !== undefined && v !== null) {
        var set;
        if (v instanceof Object) {
          set = s(v, k);
          str.push(set);
        } else if (Array.isArray(v)) {
          v.forEach(function(n) {
              set = encodeURIComponent(k) + '=' + encodeURIComponent(n);
              str.push(set);
              });
        } else {
          set = encodeURIComponent(k) + '=' + encodeURIComponent(v);
          str.push(set);
        }
      }
    }
    return str.join('&');
  };
  return s(obj, prefix);
}
```

Usage:

```javascript
var obj = {
  foo: 'bar',
  baz: 'quz'
};

console.log(serialize(obj)); // foo=bar&baz=quz
```
