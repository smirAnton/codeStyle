#  POS application Style Guide

<b>Important!</b>
<b>Use eslint with rules provided in .eslintrc (check root folder in the project)</b>

In general we follows <b>airbnb</b> rules.

Please check the most common our rules below.

# JavaScript

  1. If you must reassign references, use `let` instead of `var`.

    ```javascript
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
    ```
  2. Note that both `let` and `const` are block-scoped.

    ```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```
  3. Use object method shorthand.

    ```javascript
    // bad
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // good
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```
  4. Use property value shorthand. 

    ```javascript
    const posSystem = 'Super POS system';

    // bad
    const obj = {
      posSystem: posSystem,
    };

    // good
    const obj = {
      posSystem
    };
    ```
  5. Only quote properties that are invalid identifiers.

     ```javascript
     // bad
     const bad = {
       'foo': 3,
       'bar': 4,
       'data-blah': 5,
     };

     // good
     const good = {
       foo: 3,
       bar: 4,
       'data-blah': 5,
     };
     ```
  6. Prefer the object spread operator over to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

     ```javascript
     // very bad
     const original = { a: 1, b: 2 };
     const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
     delete copy.a; // so does this

     // bad
     const original = { a: 1, b: 2 };
     const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

     // good
     const original = { a: 1, b: 2 };
     const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

     const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
     ```
  7. Use array spreads `...` to copy arrays.

       ```javascript
       // bad
       const len = items.length;
       const itemsCopy = [];
       let i;

       for (i = 0; i < len; i += 1) {
         itemsCopy[i] = items[i];
       }

       // good
       const itemsCopy = [...items];
       ```
  8. Use array destructuring. 
    
       ```javascript
       const arr = [1, 2, 3, 4];

       // bad
       const first = arr[0];
       const second = arr[1];

       // good
       const [first, second] = arr;
       ``` 
  9.  Do not unnecessarily escape characters in strings.

    ```javascript
    // bad
    const foo = '\'this\' \i\s \"quoted\"';

    // good
    const foo = `my name is '${name}'`;
    ```
    
  10. When you must use function expressions (as when passing an anonymous function), use arrow function notation. 
  
    ```javascript
       // bad
       [1, 2, 3].map(function (x) {
         const y = x + 1;
         return x * y;
       });

       // good
       [1, 2, 3].map(x => {
         const y = x + 1;
         return x * y;
       });
    ```
  11. In modules with a single export, prefer default export over named export.

    ```javascript
    // bad
    export function foo() {}

    // good
    export default function foo() {}
    ```
    
  12.  Put all `import`s above non-import statements.

    ```javascript
    // bad
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // good
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```
    
  13. Multiline imports should be indented just like multiline array and object literals.

    ```javascript
    // bad
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // good
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```
    
  14. Avoid unneeded ternary statements.

    ```javascript
    // bad
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // good
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```
  15. Use braces with all multi-line blocks.

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function foo() { return false; }

    // good
    function bar() {
      return false;
    }
    ```
    
 # React
 
  1. If you have internal state and/or refs, prefer class extends React.Component over React.createClass unless you have a very good reason to use mixins.

    ```jsx
    // bad
    const Listing = React.createClass({
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    });

    // good
    class Listing extends React.Component {
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    }
    ```
    
  2.  If you don't have state or refs, prefer normal functions (not arrow functions) over classes:

    ```jsx
    // bad
    class Listing extends React.Component {
      render() {
        return <div>{this.props.hello}</div>;
      }
    }

    // bad (relying on function name inference is discouraged)
    const Listing = ({ hello }) => (
      <div>{hello}</div>
    );

    // good
    function Listing({ hello }) {
      return <div>{hello}</div>;
    }
    ```
    
  3. Avoid using an array index as `key` prop, prefer a unique ID. 

    ```jsx
    // bad
    {todos.map((todo, index) =>
      <Todo
        {...todo}
        key={index}
      />
    )}

    // good
    {todos.map(todo => (
      <Todo
        {...todo}
        key={todo.id}
      />
    ))}
    ```
    
  4. To bind event handlers for the render method use arrow function.

    ```jsx
    // bad
    class extends React.Component {
      onClickDiv() {
        // do stuff
      }

      render() {
        return <div onClick={this.onClickDiv.bind(this)} />
      }
    }

    // bad
    class extends React.Component {
      constructor(props) {
        super(props);

        this.onClickDiv = this.onClickDiv.bind(this);
      }

      onClickDiv() {
        // do stuff
      }

      render() {
        return <div onClick={this.onClickDiv} />
      }
    }
    
    // good
    class extends React.Component {
     
      onClickDiv = () => {
        // do stuff
      }

      render() {
        return <div onClick={this.onClickDiv} />
      }
    }
    ```
    
  5. If your component has multi-line properties, close its tag on a new line.

    ```jsx
    // bad
    <Foo
      bar="bar"
      baz="baz" />

    // good
    <Foo
      bar="bar"
      baz="baz"
    />
    ```

