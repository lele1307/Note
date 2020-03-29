# Array Object

## 构造函数

`Array`作为构造函数，行为很不一致。因此，不建议使用它生成新数组，直接使用数组字面量是更好的做法。

```javascript
// bad
var arr = new Array(1, 2);

// good
var arr = [1, 2];
```

## 静态方法

### Array.isArray()

`Array.isArray`方法返回一个布尔值，表示参数是否为数组。它可以弥补`typeof`运算符的不足。

## 实例方法

### valueOf()，toString()

- `valueOf`方法是一个所有对象都拥有的方法，表示对该对象求值。不同对象的`valueOf`方法不尽一致，数组的`valueOf`方法返回数组本身。

- `toString`方法也是对象的通用方法，数组的`toString`方法返回数组的字符串形式。

### push()，pop()

- `push`方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。

- `pop`方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组。

`push`和`pop`结合使用，就构成了“后进先出”的栈结构（stack）。

### shift()，unshift()

- `shift()`方法用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。

    `shift()`方法可以遍历并清空一个数组。

    `push()`和`shift()`结合使用，就构成了“先进先出”的队列结构（queue）。

- `unshift()`方法用于在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。

### join()

- `join()`方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

    如果数组成员是`undefined`或`null`或空位，会被转成空字符串。

    ```javascript
    [undefined, null].join('#')
    // '#'

    ['a',, 'b'].join('-')
    // 'a--b'
    ```
    通过`call`方法，这个方法也可以用于字符串或类似数组的对象。

### concat()

- `concat`方法用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。

    如果数组成员包括对象，`concat`方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是新数组拷贝的是对象的引用。

    ```javascript
    var obj = { a: 1 };
    var oldArray = [obj];

    var newArray = oldArray.concat();

    obj.a = 2;
    newArray[0].a // 2
    ```

### reverse()

- `reverse`方法用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组。

### slice()

- `slice()`方法用于提取目标数组的一部分，返回一个新数组，原数组不变。

    它的第一个参数为起始位置（从0开始，会包括在返回的新数组之中），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员。

    如果`slice()`方法的参数是负数，则表示倒数计算的位置。

    ```javascript
    var a = ['a', 'b', 'c'];
    a.slice(-2) // ["b", "c"]
    a.slice(-2, -1) // ["b"]
    ```
    
    上面代码中，`-2`表示倒数计算的第二个位置，`-1`表示倒数计算的第一个位置。

    `slice()`方法的一个重要应用，是将类似数组的对象转为真正的数组。

    ```javascript
    Array.prototype.slice.call({ 0: 'a', 1: 'b', length: 2 })
    // ['a', 'b']

    Array.prototype.slice.call(document.querySelectorAll("div"));
    Array.prototype.slice.call(arguments);
    ```


### splice()

- `splice()`方法用于删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组。

    ```javascript
    var a = ['a', 'b', 'c', 'd', 'e', 'f'];
    a.splice(4, 2, 1, 2) // ["e", "f"]
    a // ["a", "b", "c", "d", 1, 2]
    ```

    起始位置如果是负数，就表示从倒数位置开始删除。

### sort()

- `sort`方法对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。

    如果想让`sort`方法按照自定义方式排序，可以传入一个函数作为参数。

### map()

- `map`方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。

    `map`方法接受一个函数作为参数。该函数调用时，`map`方法向它传入三个参数：当前成员、当前位置和数组本身。

    ```javascript
    var numbers = [1, 2, 3];

    numbers.map(function (n) {
    return n + 1;
    });
    // [2, 3, 4]

    numbers
    // [1, 2, 3]
    ```

### forEach()

- `forEach`方法与`map`方法很相似，也是对数组的所有成员依次执行参数函数。但是，`forEach`方法不返回值，只用来操作数据。这就是说，如果数组遍历的目的是为了得到返回值，那么使用`map`方法，否则使用`forEach`方法。

`forEach`的用法与`map`方法一致，参数是一个函数，该函数同样接受三个参数：当前值、当前位置、整个数组。

`forEach`方法无法中断执行，总是会将所有成员遍历完。

`forEach`方法也会跳过数组的空位。

### filter()

`filter`方法用于过滤数组成员，满足条件的成员组成一个新数组返回。

### some()，every()

这两个方法类似“断言”（assert），返回一个布尔值，表示判断数组成员是否符合某种条件。

- `some`方法是只要一个成员的返回值是`true`，则整个`some`方法的返回值就是`true`，否则返回`false`。

- `every`方法是所有成员的返回值都是`true`，整个`every`方法才返回`true`，否则返回`false`。

对于空数组，`some`方法返回`false`，`every`方法返回`true`，回调函数都不会执行。

### reduce()，reduceRight()

`reduce`方法和`reduceRight`方法依次处理数组的每个成员，最终累计为一个值。它们的差别是，`reduce`是从左到右处理（从第一个成员到最后一个成员），`reduceRight`则是从右到左（从最后一个成员到第一个成员），其他完全一样。

`reduce`方法和`reduceRight`方法的第一个参数都是一个函数。该函数接受以下四个参数。

1. 累积变量，默认为数组的第一个成员
2. 当前变量，默认为数组的第二个成员
3. 当前位置（从0开始）
4. 原数组

### indexOf()，lastIndexOf()

- `indexOf`方法返回给定元素在数组中第一次出现的位置，如果没有出现则返回`-1`。

    `indexOf`方法还可以接受第二个参数，表示搜索的开始位置。

- `lastIndexOf`方法返回给定元素在数组中最后一次出现的位置，如果没有出现则返回`-1`。

注意，这两个方法不能用来搜索`NaN`的位置，即它们无法确定数组成员是否包含`NaN`。

### 链式使用

上面这些数组方法之中，有不少返回的还是数组，所以可以链式使用。

```javascript
var users = [
  {name: 'tom', email: 'tom@example.com'},
  {name: 'peter', email: 'peter@example.com'}
];

users
.map(function (user) {
  return user.email;
})
.filter(function (email) {
  return /^t/.test(email);
})
.forEach(function (email) {
  console.log(email);
});
// "tom@example.com"
```

上面代码中，先产生一个所有 Email 地址组成的数组，然后再过滤出以`t`开头的 Email 地址，最后将它打印出来。




