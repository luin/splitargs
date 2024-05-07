# splitargs

Splitting Redis arguments as redis-cli

## Install

```shell
$ npm install redis-splitargs
```

## Usage

```javascript
const s = require("redis-splitargs");

expect(s("set foo bar")).to.eql(["set", "foo", "bar"]);
expect(s('set "foo bar"')).to.eql(["set", "foo bar"]);
expect(s('set "foo bar\\" baz"')).to.eql(["set", 'foo bar" baz']);
expect(s("set \\  bar")).to.eql(["set", "\\", "bar"]);
expect(s("  set    foo  \r \n  bar  \v ")).to.eql(["set", "foo", "bar"]);
expect(s('"set" "foo" "bar"')).to.eql(["set", "foo", "bar"]);

expect(function () {
  s('set foo "bar');
}).to.throw();
expect(function () {
  s('set foo "bar"dsf');
}).to.throw();
expect(function () {
  s("set foo 'bar");
}).to.throw();
```
