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
