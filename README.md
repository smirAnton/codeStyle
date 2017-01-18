#  POS application JavaScript Style Guide
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
   9. Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.

    ```javascript
       // bad
       const errorMessage = 'This is a super long error that was thrown because \
       of Batman. When you stop to think about how Batman had anything to do \
       with this, you would get nowhere \
       fast.';

       // bad
       const errorMessage = 'This is a super long error that was thrown because ' +
         'of Batman. When you stop to think about how Batman had anything to do ' +
         'with this, you would get nowhere fast.';

       // good
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```
