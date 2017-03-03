## javascript 规范

### 类型
* __值类型__
  * `string`
  * `number`
  * `boolean`
  * `void`
  * `undefined`
  
```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
```
* __复杂类型__
  * `object`
  * `array`
  * `funciton`

```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
```
* * *

### 变量及常量
* __let__
```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
```
* __const__
```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
```
* __使用let和const来防止越权__
```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
```
### 对象
* __使用字面量创建对象__
```javascript
    // bad
    const item = new Object();

    // good
    const item = {};
```
* __对象方法简写__
```javascript
```













