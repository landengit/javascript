# javascript 规范

## 目录
1. [命名](#name)
1. [格式](#format)
1. [注释](#comments)
1. [类型](#types)
1. [变量及常量](#references)
1. [对象](#objects)
1. [数组](#arrays)
1. [自动拆装箱](#autoboxing)
1. [字符串](#strings)
1. [函数](#functions)
1. [箭头函数](#arrowFunctions)
1. [类](#classes)
1. [模块](#modules)
1. [集合](#collections)
1. [常用简写](#logogram)
1. [immutable](#immutable)
1. [immer](#immutable)

### <a name='name'>命名</a>
* __命名要明确，不要太简写__
```javascript
   // bad
   function q() {
     // ...
   }

   // good
   function query() {
     // ...
   }
```
* __变量使用驼峰命名法，类名第一个字母大写__
```javascript
   // bad
   const OBJEcttsssss = {};
   const this_is_my_object = {};
   function c() {}

   // good
   const thisIsMyObject = {};
   function thisIsMyFunction() {}

   // bad
   function user(options) {
     this.name = options.name;
   }

   const bad = new user({
     name: 'nope',
   });

   // good
   class User {
     constructor(options) {
       this.name = options.name;
     }
   }

   const good = new User({
     name: 'yup',
   });
```
* __包名、文件名称全小写，单词间用`-`连接__
```javascript
   // bad
   MyTitle.js
   // good
   my-title.js
```
* __名称不要使用关键字__
* __不要在代码中使用魔法数字__
```javascript
   // bad
   if(type = 1){}
   
   // good
   const user = 1;
   const master = 2;
   if(type == master){}
```

### <a name='format'>格式</a>
* __代码缩进为2个空格__
```javascript
   // bad
   function foo() {
   ∙∙∙∙let name;
   }

   // bad
   function bar() {
   ∙let name;
   }

   // good
   function baz() {
   ∙∙let name;
   }
```
* __主体代码前留1个空格__
```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    
    // good
    if(a == 1) {
      console.log('test');
    }
```
* __运算符两边要留1个空格__
```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
```
* __导入的两边要留1个空格__
```javascript
    // bad
    import {user,goods} from './project';
    // good
    import { user, goods } from './project';
```
* __太长的链式调用需要换行__
```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();
    
    // good
    $('#items')
      .find('.selected')
      .highlight()
      .end()
      .find('.open')
      .updateCount();
```
* __方法之间留1个空行__
```javascript
    // bad
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good
    const obj = {
      foo() {
      },

      bar() {
      },
    };
```
* __不要留无意义的空行__
```javascript
    // bad
    function bar() {

      console.log(foo);

    }

    // also bad
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // good
    function bar() {
      console.log(foo);
    }

    // good
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
```
* __参数逗号后跟一个空格，多的参数需要进行换行__
```javascript
    // bad
    getName('landen','li');
    
    // good
    getName('landen', 'li');
    
    // bad
    const story = [
        once
      , upon
      , aTime
    ];

    // good
    const story = [
      once,
      upon,
      aTime,
    ];
```
* __每行结尾需用`;`__
```javascript
    // bad
    (function () {
      const name = 'Skywalker'
      return name
    })()

    // good
    (function () {
      const name = 'Skywalker';
      return name;
    }());
```
* * *
### <a name='comments'>注释</a>
* __方法或类注释使用`/** ... */`__
```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
```
* __行内注释使用`//`，注释前需与前代码空一行__
```javascript
    // bad
    const active = true;  // is current tab

    // good
    // is current tab
    const active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // also good
    function getType() {
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }
```
* __注释前要留2个空格__
```javascript
    // bad
    //is current tab
    const active = true;

    // good
    // is current tab
    const active = true;

    // bad
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
```
* __待完成的使用`TODO`，有问题的使用`FIXME`__
```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn't use a global here
        total = 0;
      }
    }
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
```
* * *
### <a name='types'>类型</a>
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

### <a name='references'>变量及常量</a>
* __let__
```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    let a = 1;
    let b = 2;
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
* __使用let和const来防止变量提升__
```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
```
* __避免多余的变量定义__
```javascript
    // bad - unnecessary function call
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // good
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
```
* * * 
### <a name='objects'>对象</a>
* __使用字面量创建对象__
```javascript
    // bad
    const item = new Object();

    // good
    const item = {};
```
* __对象方法简写__
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
* __属性值一致时简写__
```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
    };
```
* __对象属性分组,简写属性列前面__
```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
```
* __简单属性无需加引号__
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
* __浅拷贝时使用ES6方式__
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
* * * 
### <a name='arrays'>数组</a>
* __使用字面量创建对象__
```javascript
    // bad
    const items = new Array();

    // good
    const items = [];
```
* __使用`push`代替根据下标添加值__
```javascript
    const someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
```
* __复制数组使用ES6的`...`__
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
* __使用`Array.from`来转换类数组(伪数组)__
```javascript
    const foo = document.querySelectorAll('.foo');
    const nodes = Array.from(foo);
```
* __循环时正确的写法__
```javascript
    // good 
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // good 
    [1, 2, 3].map(x => x + 1);

    // bad
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
    });

    // good
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
      return flatten;
    });

    // bad
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // good
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
```
* * *
### <a name='autoboxing'>自动拆装箱</a>
* __使用对象的自动拆包__
```javascript
    // bad
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // good
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // best
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
```
* __使用数组的自动拆包__
```javascript
    const arr = [1, 2, 3, 4];

    // bad
    const first = arr[0];
    const second = arr[1];

    // good
    const [first, second] = arr;
```
* __返回对象使用装包时,使用对象转包,不要使用数组__
```javascript
    // bad
    function processInput(input) {
      // then a miracle occurs
      return [left, right, top, bottom];
    }

    // the caller needs to think about the order of return data
    const [left, __, top] = processInput(input);

    // good
    function processInput(input) {
      // then a miracle occurs
      return { left, right, top, bottom };
    }

    // the caller selects only the data they need
    const { left, top } = processInput(input);
```
* * *
### <a name='strings'>字符串</a>
* __对字符串使用单引号`''`__
```javascript
    // bad
    const name = "Capt. Janeway";

    // bad - template literals should contain interpolation or newlines
    const name = `Capt. Janeway`;

    // good
    const name = 'Capt. Janeway';
```
* __字符串过长时应该换行__
```javascript
    // bad
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // bad
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // good
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
```
* __变量替换使用`${}`__
```javascript
    // bad
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // bad
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // bad
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // good
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
```
* __引号替换__
```javascript
    // bad
    const foo = '\'this\' \i\s \"quoted\"';

    // good
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
```
* * *
### <a name='functions'>函数</a>
* __函数声明__
```javascript
    // 匿名函数表达式
    var anonymous = function() {
      return true;
    };

    // 有名函数表达式
    var named = function named() {
      return true;
    };

    // 立即调用函数表达式
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
```
* __不要在代码块里定义方法__
```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
```
* __不要将方法名定义为`arguments`__
```javascript
    // bad
    function foo(name, options, arguments) {
      // ...
    }

    // good
    function foo(name, options, args) {
      // ...
    }
```
* __不要手动解析`arguments`，使用自动拆包__
```javascript
    // bad
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // good
    function concatenateAll(...args) {
      return args.join('');
    }
```
* __参数必传时，使用默认值__
```javascript
    // really bad
    function handleThings(opts) {
      // No! We shouldn't mutate function arguments.
      // Double bad: if opts is falsy it'll be set to an object which may
      // be what you want but it can introduce subtle bugs.
      opts = opts || {};
      // ...
    }

    // still bad
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // good
    function handleThings(opts = {}) {
      // ...
    }
```
* __避免不可控的默认参数__
```javascript
    var b = 1;
    // bad
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
```
* __有默认值的参数放最后__
```javascript
    // bad
    function handleThings(opts = {}, name) {
      // ...
    }

    // good
    function handleThings(name, opts = {}) {
      // ...
    }
```
* __不要使用`Function`来创建方法__
```javascript
    // bad
    var add = new Function('a', 'b', 'return a + b');

    // still bad
    var subtract = Function('a', 'b', 'return a - b');

    // good
    var x = function (a, b) {
        return a + b;
    };
```
* * *
### <a name='arrowFunctions'>箭头函数</a>
* __当你的参数是个函数时可使用箭头函数`Arrow functions`__
```javascript
    // bad
    [1, 2, 3].map(number => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // good
    [1, 2, 3].map(number => `A string containing the ${number}.`);

    // good
    [1, 2, 3].map(number => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });
```
* __方法体是多行或者带运算符时，用括号包起来__
```javascript
   // bad
   ['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
       httpMagicObjectWithAVeryLongName,
       httpMethod,
     )
   );

   // good
   ['get', 'post', 'put'].map(httpMethod => (
     Object.prototype.hasOwnProperty.call(
       httpMagicObjectWithAVeryLongName,
       httpMethod,
     )
   ));
   
   // bad
   const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

   // bad
   const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

   // good
   const itemHeight = item => (item.height > 256 ? item.largeSize : item.smallSize);

   // good
   const itemHeight = (item) => {
     const { height, largeSize, smallSize } = item;
     return height > 256 ? largeSize : smallSize;
   };
```
* __参数只有一个时，不要使用括号__
```javascript
   // bad
   [1, 2, 3].map((x) => x * x);

   // good
   [1, 2, 3].map(x => x * x);
```
* * *

### <a name='classes'>类</a>
* __类初始化使用`constructor`__
```javascript
    // bad
    [1, 2, 3].map((x) => x * x);

    // good
    [1, 2, 3].map(x => x * x);
```
* __继承使用`extends`__
```javascript
    // bad
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // good
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
```
* * *
### <a name='modules'>模块</a>
* __导入模块时要清晰明了，不要使用`*`__
```javascript
// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
module.exports = AirbnbStyleGuide.es6;

// bad
import * as AirbnbStyleGuide from './AirbnbStyleGuide';

// ok
import AirbnbStyleGuide from './AirbnbStyleGuide';
export default AirbnbStyleGuide.es6;

// best
import { es6 } from './AirbnbStyleGuide';
export default es6;
```
* __不要在导入的同时导出__
```javascript
    // bad
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // good
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
```
* __同一模块的导入不要拆开写__
```javascript
    // bad
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // good
    import foo, { named1, named2 } from 'foo';

    // good
    import foo, {
      named1,
      named2,
    } from 'foo';
```
* __导入分组放在一起__
```javascript
    // 先导入公共依赖，再导入本地模块
    import React, {Component} from 'react';
    import {Tabbar} from 'qmkit';
    import {StoreProvider, msg} from 'iflux2';
    import AppStore from './store';
    import Tip from './component/tip';
```
* __太长的导入换行__
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
* * *
### <a name='collections'>集合</a> [immutable](http://facebook.github.io/immutable-js)
* __遍历使用 `foreach` / `map`__
```javascript
    import Immutable = require('immutable');
    
    let map1: Immutable.Map<string, number>;
    map1 = Immutable.Map({a:1, b:2, c:3});
    
    map1.foreach(item => {...});
    map1.map(item => {...});
```
* __取值/赋值__
```javascript
    import Immutable = require('immutable');
    
    let map1: Immutable.Map<string, number>;
    map1 = Immutable.Map({a:1, b:2, c:3});
    let map2 = map1.set('b', 50);
    map1.get('b'); // 2
    map2.get('b'); // 50
```
* * *
### <a name='logogram'>常用简写</a>
* __判断简写__
```javascript
    // bad
    if (isValid === true) {
      // ...
    }

    // good
    if (isValid) {
      // ...
    }

    // good
    if (name) {
      // ...
    }

    // good
    if (collection.length) {
      // ...
    }
```
* __三元表达式__
```javascript
    // bad
    let count = 1;
    if (isValid) {
      count = 2;
    }

    // good
    let count = isValid ? 2 : 1;
```
* __可替代三元表达式的情况__
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
* * *
### <a name='immutable'>immutable</a>
* __初始化__
```javascript
    // list
    const list = List();
    const list = List([1, 2, 3]);

    // map
    const map = Map();
    const map = Map({a: 1, b: 2});
    
    // 转换后map的key为string类型，获取值需要get('...')
    const a = map.get('a');

```
* __转换__
```javascript
    // 
    const list = [1, 2, 3];
    const map = {a: 1, b: 2};
    
    // 方法1
    const immutable_list = List(list);
    const immutable_map = Map(map);
    
    // 方法2
    const immutable_list = fromJS(list);
    const immutable_map = fromJS(map);

    // 负责类型时推荐使用方法2，方法1转换时只会转换最外层，内层还是原类型
    const map = {a: 1, b: 2, c: [1, 2]};
    const immutable_map = Map(map);
    const immutable_map2 = fromJS(map);
    console.log(immutable_map.get('c')); // [1, 2]
    console.log(immutable_map2.get('c'));// List {size: 2, _origin: 0, _capacity: 2, _level: 5, _root: null…}
    
```
* __在何时转换：推荐在store转换，保证actor和组件接触到的值都是inmmutable类型__
* __获取长度__
```javascript
    
    const list = List([1, 2, 3]);
    const map = Map({a: 1, b: 2, c: 3});
    
    // bad
    const count = list.size;
    const count = map.size;

    // good
    const count = list.count();
    const count = map.count();
```
* __获取多层内容__
```javascript
    
    const map = fromJS({a: 1, b: 2, c: {d: 3, e: 4}});
    
    // bad
    const d = map.get('c').get('d');

    // good
    const d = map.getIn(['c', 'd']);
```
* __修改值__
```javascript
    
    const list = List([1, 2, 3]);
    const map = Map({a: 1, b: 2, c: 3});
    
    // good
    let list = list.set(0, 10);
    let map = map.set('a', 10);
    
    // good
    let list= list.update(0, value => value * value);
    let map = map.update('a', value => value * value);

```
* __修改多层级的值__
```javascript

    const map = fromJS({a: 1, b: 2, c: {d: 3, e: 4}});
    
    // good
    let map = map.updateIn(['c','d'], 10);

```
* __操作都是不可变__
```javascript

    const list = List([1, 2, 3]);

    list.push(4);
    list.push(5);
    list.push(6);
    console.log(list.toJS()); // [1, 2, 3]

    list = list.push(4);
    list = list.push(5);
    list = list.push(6);
    console.log(list.toJS()); // [1, 2, 3, 4, 5, 6]
    
```
* __遍历__
```javascript

    const list = List([1, 2, 3]);
    const map = Map({a: 1, b: 2, c: 3});

    // bad
    for(let i = 0; i < list.count(); i++){
      ...
    }

    // good
    list.forEach(item => {
      ....
    })
    
    map.forEach((value, key) => {
      ...
    })
```















































