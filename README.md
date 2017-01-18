# POS application
# Code Style

1. If you must reassign references, use let instead of var. eslint: no-var jscs: disallowVar

// bad<br/>
var count = 1;<br/>
if (true) {<br/>
  count += 1;<br/>
}<br/>

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}
