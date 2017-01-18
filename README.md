# POS application
# Code Style

1. If you must reassign references, use let instead of var. eslint: no-var jscs: disallowVar

// bad

var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}
