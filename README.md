

# 数字编码



## 1. 原码、反码和补码

**`首先需要指出，数字是以补码的形式存储在计算机中的。在分析这样做的原因之前，首先给出三者的定义。`** 

* **`原码：我们将数字的二进制表示的最高位视为符号位，其中 0 表示正数，1 表示负数，其余位表示数字的值。`** 
* **`反码：正数的反码与其原码相同，负数的反码是对其原码除符号位外的所有位取反。`** 
* **`补码：正数的补码与其原码相同，负数的补码是在其反码的基础上加 1。`** 



**`如图所示展示了原码、反码和补码之间的转换方法。`** 

![](https://www.hello-algo.com/chapter_data_structure/number_encoding.assets/1s_2s_complement.png)

**`原码虽然最直观，但存在一些局限性。一方面，负数的原码不能直接用于运算。例如在原码下计算 1 + (-2) ，得到的结果是 -3，这显然是不对的。`** 

```javascript
1 + (-2)
0000 0001 + 1000 0010
-3
```

**`为了解决此问题，计算机引入了反码。如果我们先将原码转换为反码，并在反码下计算 1 + (-2)，最后将结果从反码转换回原码，则可得到正确结果 -1。`** 

```javascript
1 + (-2)
0000 0001（原码）+ 1000 0010（原码）
0000 0001（反码）+ 1111 1101（反码）
1111 1110（反码）
1000 0001（原码）
-1
```

**`另一方面，数字零的原码有 +0 和 -0 两种表示方式。这意味着数字零对应两个不同的二进制编码，这可能会带来歧义。比如在条件判断中，如果没有区分正零和负零，则可能会导致判断结果出错。而如果我们想处理正零和负零歧义，则需要引入额外的判断操作，这可能会降低计算机的运算效率。`** 

```javascript
+0 => 0000 0000
-0 => 1000 0000
```



**`与原码一样，反码也存在正负零歧义问题，因此计算机进一步引入了补码。我们先来观察一下负零的原码、反码、补码的转换过程：`** 

```javascript
-0 => 1000 0000（原码）
1111 1111（反码）
1 0000 0000（补码）
```

**`在负零的反码基础上加 1 会产生进位，但 byte 类型的长度只有 8 位，因此溢出到第 9 位的 1 会被舍弃。也就是说，负零的补码为 0000 0000，与正零的补码相同。这意味着在补码表示中只存在一个零，正负零歧义从而得到解决。`**

**`还剩最后一个疑惑：byte 类型的取值范围是 [-128, 127]，多出来的一个负数 -128 是如何得到的呢？我们注意到，区间 [-127, +127] 内的所有整数都有对应的原码、反码和补码，并且原码和补码之间可以互相转换。`** 

**`然而，补码 1000 0000 是一个例外，它并没有对应的原码。根据转换方法，我们得到该补码的原码为 0000 0000。这显然是矛盾的，因为该原码表示数字 0，它的补码应该是自身。计算机规定这个特殊的补码 1000 0000 代表 -128。实际上，（-1）+ （-127）在补码下的计算结果就是 -128。`** 

```javascript
(-127) + (-1)
-> 1111 1111（原码）+ 1000 0001（原码）
= 1000 0000（反码）+ 1111 1110（反码）
= 1000 0001（补码）+ 1111 1111（补码）
= 1000 0000（补码）
= -128
```









# 字符编码



## 1. ASCII 字符集

**`ASCII 码是最早出现的字符集，其全称为 American Standard Code for Information Interchange（美国标准信息交换代码）。它使用 7 位二进制数（一个字节的低 7 位）表示一个字符，最多能够表示 128 个不同的字符。如下图所示，ASCII 码包括英文字母的大小写、数字 0 ~ 9、一些标点符号，以及一些控制字符（如换行符和制表符）。`**

![](https://www.hello-algo.com/chapter_data_structure/character_encoding.assets/ascii_table.png)

**`然而，ASCII 码仅能够表示英文。随着计算机的全球化，诞生了一种能够表示更多语言的 EASCII 字符集。它在 ASCII 的 7 位基础上扩展到 8 位，能够表示 256 个不同的字符。在世界范围内，陆续出现了一批适用于不同地区的 EASCII 字符集。这些字符集的前 128 个字符统一为 ASCII 码，后 128 个字符定义不同，以适应不同语言的需求。`**





## 2. GBK 字符集

**`后来人们发现，EASCII 码仍然无法满足许多语言的字符数量要求。比如汉字有近十万个，光日常使用的就有几千个。中国国家标准总局于 1980 年发布了  GB2312 字符集，其收录了 6763 个汉字，基本满足了汉字的计算机处理需要。然而，GB2312 无法处理部分罕见字和繁体字。GBK 字符集是在 GB2312 的基础上扩展得到的，它共收录了 21886 个汉字。在 GBK 的编码方案中，ASCII 字符使用一个字节表示，汉字使用两个字节表示。`** 





## 3. Unicode 字符集

**`随着计算机技术的蓬勃发展，字符集与编码标准百花齐放，而这带来了许多问题。一方面，这些字符集一般只定义了特定语言的字符，无法在多语言环境下正常工作。另一方面，同一种语言存在多种字符集标准，如果两台计算机使用的是不同的编码标准，则在信息传递时就会出现乱码。`** 

**`那个时代的研究人员就在想：如果推出一个足够完整的字符集，将世界范围内的所有语言和符号都收录其中，不就可以解决跨语言环境和乱码问题了吗？在这种想法的驱动下，一个大而全的字符集 Unicode 应运而生。`** 

**`Unicode 的中文名称为统一码，理论上能容纳 100 多万个字符。它致力于将全球范围内的字符纳入统一的字符集之中，提供一种通用的字符集来处理和显示各种语言文字，减少因为编码标准不同而产生的乱码问题。`** 

**`自 1991 年发布以来，Unicode 不断扩充新的语言与字符。截至 2022 年 9 月，Unicode 已经包含 149186 个字符，包含各种语言的字符、符号甚至表情符号等。在庞大的 Unicode 字符集中，常用的字符占用 2 个字节，有些生僻的字符占用 3 字节甚至 4 字节。`** 

**`Unicode 是一种通用字符集，本质上是给每个字符分配一个编号（称为码点），但它并没有规定在计算机中如何存储这些字符码点。我们不禁会问：当多种长度的 Unicode 码点同时出现在一个文本中时，系统如何解析字符？例如给定一个长度为 2 字节的编码，系统如何确认它是一个 2 字节的字符还是两个 1 字节的字符？`** 

**`对于以上问题，一种直接的解决方案是将所有字符存储为等长的编码。如图所示，"Hello" 中的每个字符占用 1 字节，算法中的每个字符占用 2 字节。我们可以通过高位填 0 将 Hello 算法中的所有字符都编码为 2 字节长度。这样系统就可以每隔 2 字节解析一个字符，恢复这个短语的内容了。`** 

![](https://www.hello-algo.com/chapter_data_structure/character_encoding.assets/unicode_hello_algo.png)

**`然而 ASCII 码已经向我们证明，编码英文只需 1 字节。若采用上述方案，英文文本占用空间的大小将会是 ASCII 编码下的两倍，非常浪费内存空间。因此，我们需要一种更加高效的 Unicode 编码方法。`** 





## 4. UTF-8 编码

**`目前，UTF-8 已成为国际上使用最广泛的 Unicode 编码方法。它是一种可变长度的编码，使用 1 到 4 字节来表示一个字符，根据字节的复杂性而变。ASCII 字符只需 1 字节，拉丁字母和希腊字母需要 2 字节，常用的中文字符需要 3 字节，其他的一些生僻字符需要 4 字节。`** 

**`UTF-8 的编码规则并不复杂，分为以下两种情况。`** 

* **`对于长度为 1 字节的字符，将最高位设置为 0，其余 7 位设置为 Unicode 码点。值得注意的是，ASCII 字符在 Unicode 字符集中占据了前 128 个码点。也就是说，UTF-8 编码可以向下兼容 ASCII 码。这意味着我们可以使用 UTF-8 来解析年代久远的 ASCII 码文本。`** 
* **`对于长度为 n 字节的字符（其中 n > 1），将首个字节的高 n 位都设置为 1，第 n + 1 位设置为 0；从第二个字节开始，将每个字符的高 2 位的设置为 10；其余所有位用于填充字符的 Unicode 码点。`** 

![](https://www.hello-algo.com/chapter_data_structure/character_encoding.assets/utf-8_hello_algo.png)

**`除了 UTF-8 之外，常见的编码方式还包括以下两种。`** 

* **`UTF-16 编码：使用 2 或 4 字节来表示一个字符。所有的 ASCII 字符和常用的非英文字符，都用 2 字节表示；少数字符需要用到 4 字节表示。对于 2 字节的字符，UTF-16 编码与 Unicode 码点相等。`** 
* **`UTF-32 编码：每个字符都使用 4 字节。这意味着 UTF-32 比 UTF-8 和 UTF-16 更占用空间，特别是对于 ASCII 字符占比较高的文本。`** 

**`从存储空间占用的角度看，使用 UTF-8 表示英文字符非常高效，因为它仅需 1 字节；使用 UTF-16 编码某些非英文字符（例如中文）会更加高效，因为它仅需 2 字节，而 UTF-8 可能需要 3 字节。`** 

**`从兼容性的角度看，UTF-8 的通用性最佳，许多工具和库优先支持 UTF-8。`** 













# 数组

## 1. `push()`

```javascript
let fruits = ["apple", "banana"];
let newLength = fruits.push("orange", "mango");
console.log(fruits); // 输出: ["apple", "banana", "orange", "mango"]
console.log(newLength); // 输出: 4
```





## 2. `pop()`

**`删除数组的最后一个元素，并返回该元素的值。如果数组为空，则返回 undefined。`**

```javascript
let fruits = ["apple", "banana", "orange"];
let lastFruit = fruits.pop();
console.log(fruits); // 输出: ["apple", "banana"]
console.log(lastFruit); // 输出: "orange"
```



## 3. `shift()`

**`删除数组的第一个元素，并返回该元素的值。如果数组为空，则返回 undefined。`**

```javascript
let fruits = ["apple", "banana", "orange"];
let firstFruit = fruits.shift();
console.log(fruits); // 输出: ["banana", "orange"]
console.log(firstFruit); // 输出: "apple"
```





## 4. `unshift()`

**`将一个或多个元素添加到数组的开头，并返回修改后的数组的新长度。`**

```javascript
let fruits = ["banana", "orange"];
let newLength = fruits.unshift("apple", "mango");
console.log(fruits); // 输出: ["apple", "mango", "banana", "orange"]
console.log(newLength); // 输出: 4
```





## 5. `splice()`

**`通过删除或替换现有元素或者原地添加新的元素来修改数组。`**

```javascript
let fruits = ["apple", "banana", "orange", "mango"];

// 从索引 2 开始删除 1 个元素，并添加 "grape"
let removed = fruits.splice(2, 1, "grape");
console.log(fruits); // 输出: ["apple", "banana", "grape", "mango"]
console.log(removed); // 输出: ["orange"]

// 从索引 1 开始删除 0 个元素，并添加 "kiwi" 和 "melon"
fruits.splice(1, 0, "kiwi", "melon");
console.log(fruits); // 输出: ["apple", "kiwi", "melon", "banana", "grape", "mango"]

// 从索引 3 开始删除到数组末尾的所有元素
fruits.splice(3);
console.log(fruits); // 输出: ["apple", "kiwi", "melon"]
```





## 6. `concat()`

**`用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。`**

```javascript
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let arr3 = [7, 8, 9];

let combined = arr1.concat(arr2, arr3);
console.log(combined); // 输出: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```



## 7. `every()`

**`测试一个数组中的所有元素是否都能通过指定函数的测试。它返回一个布尔值。`**

```javascript
let numbers = [1, 2, 3, 4, 5];

let allPositive = numbers.every(num => num > 0);
console.log(allPositive); // 输出: true

let allEven = numbers.every(num => num % 2 === 0);
console.log(allEven); // 输出: false
```





## 8. `filter()`

**`创建一个新数组，其包含通过所提供函数实现的测试的所有元素。`**

```javascript
let numbers = [1, 2, 3, 4, 5];

let evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // 输出: [2, 4]

let oddNumbers = numbers.filter(num => num % 2 !== 0);
console.log(oddNumbers); // 输出: [1, 3, 5]
```





## 9. `forEach()`

**`对数组的每个元素执行一次给定的函数。`**

```javascript
let fruits = ["apple", "banana", "orange"];

fruits.forEach(fruit => {
  console.log("I like " + fruit);
});
// 输出:
// I like apple
// I like banana
// I like orange
```





## 10. `join()`

**`将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。你可以使用一个分隔符来分隔数组元素。如果省略 separator，数组元素将用逗号（,）分隔。`**

```javascript
let fruits = ["apple", "banana", "orange"];

let joinedString = fruits.join(", ");
console.log(joinedString); // 输出: "apple, banana, orange"

let joinedString2 = fruits.join(" - ");
console.log(joinedString2); // 输出: "apple - banana - orange"
```





## 11. `indexOf()`

**`返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回 -1。`**

```javascript
let fruits = ["apple", "banana", "orange", "banana"];

let index1 = fruits.indexOf("banana");
console.log(index1); // 输出: 1

let index2 = fruits.indexOf("grape");
console.log(index2); // 输出: -1

let index3 = fruits.indexOf("banana", 2); // 从索引 2 开始搜索
console.log(index3); // 输出: 3
```





## 12. `lastIndexOf()`

**`返回在数组中可以找到一个给定元素的最后一个索引，如果不存在，则返回 -1。从数组的后面向前搜索，从 fromIndex 处开始。`**

```javascript
let fruits = ["apple", "banana", "orange", "banana"];

let index1 = fruits.lastIndexOf("banana");
console.log(index1); // 输出: 3

let index2 = fruits.lastIndexOf("grape");
console.log(index2); // 输出: -1

let index3 = fruits.lastIndexOf("banana", 2); // 从索引 2 开始向前搜索
console.log(index3); // 输出: 1
```





## 13. `map()`

**`创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。`**

```javascript
let numbers = [1, 2, 3, 4, 5];

let squaredNumbers = numbers.map(num => num * 2);
console.log(squaredNumbers); // 输出: [2, 4, 6, 8, 10]
```





## 14. `reverse()`

**`将数组中元素的位置颠倒，并返回该数组。该方法会改变原数组。`**

```javascript
let fruits = ["apple", "banana", "orange"];

fruits.reverse();
console.log(fruits); // 输出: ["orange", "banana", "apple"]
```





## 15. `slice()`

**`返回一个新的数组对象，这一对象是一个由 start 和 end 决定的原数组的浅拷贝（包括 start，不包括 end）。原始数组不会被修改。`**

```javascript
let fruits = ["apple", "banana", "orange", "mango"];

let slicedArray = fruits.slice(1, 3);
console.log(slicedArray); // 输出: ["banana", "orange"]

let slicedArray2 = fruits.slice(2); // 从索引 2 开始到数组末尾
console.log(slicedArray2); // 输出: ["orange", "mango"]

let slicedArray3 = fruits.slice(); // 复制整个数组
console.log(slicedArray3); // 输出: ["apple", "banana", "orange", "mango"]
```



## 16. `some()`

**`测试数组中是不是至少有 1 个元素通过了被提供的函数测试。它返回的是一个 Boolean 类型的值。`**

```javascript
let numbers = [1, 2, 3, 4, 5];

let hasEvenNumber = numbers.some(num => num % 2 === 0);
console.log(hasEvenNumber); // 输出: true

let hasNegativeNumber = numbers.some(num => num < 0);
console.log(hasNegativeNumber); // 输出: false
```





## 17. `sort()`

**`对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的 UTF-16 代码单元值序列时构建的。`**

```javascript
let fruits = ["orange", "apple", "banana"];

fruits.sort();
console.log(fruits); // 输出: ["apple", "banana", "orange"]

let numbers = [10, 5, 8, 1, 7];

numbers.sort((a, b) => a - b); // 升序排序
console.log(numbers); // 输出: [1, 5, 7, 8, 10]

numbers.sort((a, b) => b - a); // 降序排序
console.log(numbers); // 输出: [10, 8, 7, 5, 1]
```





## 18. `toString()`

**`返回一个字符串，表示指定的数组及其元素。`**

```javascript
let fruits = ["apple", "banana", "orange"];

let stringRepresentation = fruits.toString();
console.log(stringRepresentation); // 输出: "apple,banana,orange"
```





## 19. `valueOf()`

**`返回数组对象的原始值。`**

```javascript
let fruits = ["apple", "banana", "orange"];

let arrayValue = fruits.valueOf();
console.log(arrayValue); // 输出: ["apple", "banana", "orange"]

console.log(arrayValue === fruits); // 输出: true (返回的是数组本身)
```



## 20. `@@iterator 对象`

**`@@iterator 方法是数组的默认迭代器，它返回一个新的 Array Iterator 对象，该对象可以按顺序访问数组中的每个元素。`**

```javascript
const arr = ['a', 'b', 'c'];
const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // 输出: { value: 'a', done: false }
console.log(iterator.next()); // 输出: { value: 'b', done: false }
console.log(iterator.next()); // 输出: { value: 'c', done: false }
console.log(iterator.next()); // 输出: { value: undefined, done: true }
```





## 21. `copyWithin()`

**`浅复制数组的一部分到同一数组中的另一个位置，并返回修改后的数组，不会改变数组的长度。`**

```javascript
const arr = [1, 2, 3, 4, 5];

// 从索引 3 开始复制到索引 0
arr.copyWithin(0, 3, 5);
console.log(arr); // 输出: [4, 5, 3, 4, 5]

// 从索引 2 开始复制到索引 1
arr.copyWithin(1, 2);
console.log(arr); // 输出: [4, 3, 4, 4, 5]
```





## 22. `entries()`

**`返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键值对。`**

```javascript
const arr = ['a', 'b', 'c'];
const iterator = arr.entries();

console.log(iterator.next().value); // 输出: [0, 'a']
console.log(iterator.next().value); // 输出: [1, 'b']
console.log(iterator.next().value); // 输出: [2, 'c']
console.log(iterator.next().done);  // 输出: true
```





## 23. `includes()`

**`用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false。`**

```javascript
const arr = [1, 2, 3, 4, 5];

console.log(arr.includes(3)); // 输出: true
console.log(arr.includes(6)); // 输出: false
console.log(arr.includes(3, 2)); // 从索引 2 开始查找，输出: true
console.log(arr.includes(3, 3)); // 从索引 3 开始查找，输出: false
```





## 24. `find()`

**`返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。`**

```javascript
const arr = [10, 20, 30, 40, 50];

const found = arr.find(element => element > 25);
console.log(found); // 输出: 30

const notFound = arr.find(element => element > 60);
console.log(notFound); // 输出: undefined
```



## 25. `findIndex()`

**`返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回 -1。`**

```javascript
const arr = [10, 20, 30, 40, 50];

const foundIndex = arr.findIndex(element => element > 25);
console.log(foundIndex); // 输出: 2

const notFoundIndex = arr.findIndex(element => element > 60);
console.log(notFoundIndex); // 输出: -1
```





## 26. `fill()`

**`用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。返回修改后的数组。`**

```javascript
const arr = [1, 2, 3, 4, 5];

// 用 0 填充整个数组
arr.fill(0);
console.log(arr); // 输出: [0, 0, 0, 0, 0]

const arr2 = [1, 2, 3, 4, 5];

// 用 0 从索引 2 开始填充到数组末尾
arr2.fill(0, 2);
console.log(arr2); // 输出: [1, 2, 0, 0, 0]

const arr3 = [1, 2, 3, 4, 5];

// 用 0 从索引 1 开始填充到索引 3 (不包括索引 3)
arr3.fill(0, 1, 3);
console.log(arr3); // 输出: [1, 0, 0, 4, 5]
```





## 27. `Array.from()`

**`从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。`**

```javascript
// 从字符串创建数组
const str = "hello";
const arr1 = Array.from(str);
console.log(arr1); // 输出: ["h", "e", "l", "l", "o"]

// 从 Set 创建数组
const set = new Set([1, 2, 3, 4, 5]);
const arr2 = Array.from(set);
console.log(arr2); // 输出: [1, 2, 3, 4, 5]

// 使用 mapFn
const numbers = [1, 2, 3, 4, 5];
const arr3 = Array.from(numbers, x => x * 2);
console.log(arr3); // 输出: [2, 4, 6, 8, 10]
```



## 28. `keys()`

**`返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键。`**

```javascript
const arr = ['a', 'b', 'c'];
const iterator = arr.keys();

console.log(iterator.next().value); // 输出: 0
console.log(iterator.next().value); // 输出: 1
console.log(iterator.next().value); // 输出: 2
console.log(iterator.next().done);  // 输出: true
```



## 29. `Array.of()`

**`创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。`**

```javascript
const arr1 = Array.of(1, 2, 3);
console.log(arr1); // 输出: [1, 2, 3]

const arr2 = Array.of("a", "b", "c");
console.log(arr2); // 输出: ["a", "b", "c"]

const arr3 = Array.of(7); // 创建一个包含单个元素 7 的数组
console.log(arr3); // 输出: [7]

const arr4 = Array.of(1, 'a', true);
console.log(arr4); // 输出: [1, "a", true]
```



## 30. `values()`

**`返回一个新的 Array Iterator 对象，该对象包含数组每个索引的值`**。

```javascript
const arr = ['a', 'b', 'c'];
const iterator = arr.values();

console.log(iterator.next().value); // 输出: 'a'
console.log(iterator.next().value); // 输出: 'b'
console.log(iterator.next().value); // 输出: 'c'
console.log(iterator.next().done);  // 输出: true
```











# 栈



## 1. 栈数据结构

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  // 入栈：将元素添加到栈的顶部
  push(element) {
    this.items.push(element);
  }

  // 出栈：移除栈顶部的元素并返回
  pop() {
    if (this.isEmpty()) {
      return "栈为空";
    }
    return this.items.pop();
  }

  // 查看栈顶部的元素
  peek() {
    if (this.isEmpty()) {
      return "栈为空";
    }
    return this.items[this.items.length - 1];
  }

  // 检查栈是否为空
  isEmpty() {
    return this.items.length === 0;
  }

  // 获取栈的大小
  size() {
    return this.items.length;
  }

  // 清空栈
  clear() {
    this.items = [];
  }
}

// 示例用法
const stack = new Stack();

stack.push(10);
stack.push(20);
stack.push(30);

console.log("栈顶元素:", stack.peek()); // 输出: 30
console.log("出栈:", stack.pop()); // 输出: 30
console.log("栈的大小:", stack.size()); // 输出: 2
console.log("栈是否为空:", stack.isEmpty()); // 输出: false

stack.clear();
console.log("栈是否为空 (清空后):", stack.isEmpty()); // 输出: true
```







## 2. 创建一个基于 JavaScript 对象的 Stack 类

```javascript
class Stack {
  constructor() {
    this.items = {}; // 使用对象存储栈元素
    this.count = 0;  // 记录栈的大小
  }

  // 入栈：将元素添加到栈的顶部
  push(element) {
    this.items[this.count] = element;
    this.count++;
  }

  // 出栈：移除栈顶部的元素并返回
  pop() {
    if (this.isEmpty()) {
      return "栈为空";
    }
    this.count--;
    const result = this.items[this.count];
    delete this.items[this.count]; // 移除对象中的属性
    return result;
  }

  // 查看栈顶部的元素
  peek() {
    if (this.isEmpty()) {
      return "栈为空";
    }
    return this.items[this.count - 1];
  }

  // 检查栈是否为空
  isEmpty() {
    return this.count === 0;
  }

  // 获取栈的大小
  size() {
    return this.count;
  }

  // 清空栈
  clear() {
    this.items = {};
    this.count = 0;
  }
}

// 示例用法
const stack = new Stack();

stack.push(10);
stack.push(20);
stack.push(30);

console.log("栈顶元素:", stack.peek()); // 输出: 30
console.log("出栈:", stack.pop()); // 输出: 30
console.log("栈的大小:", stack.size()); // 输出: 2
console.log("栈是否为空:", stack.isEmpty()); // 输出: false

stack.clear();
console.log("栈是否为空 (清空后):", stack.isEmpty()); // 输出: true
```









# 队列和双端队列



## 1. 队列数据结构

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  // 入队：将元素添加到队列的尾部
  enqueue(element) {
    this.items.push(element);
  }

  // 出队：移除队列头部的元素并返回
  dequeue() {
    if (this.isEmpty()) {
      return "队列为空";
    }
    return this.items.shift();
  }

  // 查看队列头部的元素
  peek() {
    if (this.isEmpty()) {
      return "队列为空";
    }
    return this.items[0];
  }

  // 检查队列是否为空
  isEmpty() {
    return this.items.length === 0;
  }

  // 获取队列的大小
  size() {
    return this.items.length;
  }

  // 清空队列
  clear() {
    this.items = [];
  }
}

// 示例用法
const queue = new Queue();

queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);

console.log("队列头部元素:", queue.peek()); // 输出: 10
console.log("出队:", queue.dequeue()); // 输出: 10
console.log("队列大小:", queue.size()); // 输出: 2
console.log("队列是否为空:", queue.isEmpty()); // 输出: false

queue.clear();
console.log("队列是否为空 (清空后):", queue.isEmpty()); // 输出: true
```





## 2. 双端队列

```javascript
class Deque {
  constructor() {
    this.items = [];
  }

  // 从队列头部添加元素
  addFront(element) {
    this.items.unshift(element);
  }

  // 从队列尾部添加元素
  addBack(element) {
    this.items.push(element);
  }

  // 从队列头部移除元素
  removeFront() {
    if (this.isEmpty()) {
      return "双端队列为空";
    }
    return this.items.shift();
  }

  // 从队列尾部移除元素
  removeBack() {
    if (this.isEmpty()) {
      return "双端队列为空";
    }
    return this.items.pop();
  }

  // 查看队列头部的元素
  peekFront() {
    if (this.isEmpty()) {
      return "双端队列为空";
    }
    return this.items[0];
  }

  // 查看队列尾部的元素
  peekBack() {
    if (this.isEmpty()) {
      return "双端队列为空";
    }
    return this.items[this.items.length - 1];
  }

  // 检查队列是否为空
  isEmpty() {
    return this.items.length === 0;
  }

  // 获取队列的大小
  size() {
    return this.items.length;
  }

  // 清空队列
  clear() {
    this.items = [];
  }
}

// 示例用法
const deque = new Deque();

deque.addFront(10);
deque.addBack(20);
deque.addFront(5);
deque.addBack(30);

console.log("双端队列头部元素:", deque.peekFront()); // 输出: 5
console.log("双端队列尾部元素:", deque.peekBack()); // 输出: 30
console.log("从头部移除:", deque.removeFront()); // 输出: 5
console.log("从尾部移除:", deque.removeBack()); // 输出: 30
console.log("双端队列大小:", deque.size()); // 输出: 2
```











# 链表

**`如以下代码所示，链表节点 ListNode 除了包含值，还需额外保存一个引用（指针）。因此在相同数据量下，链表比数组占用更多的内存空间。`** 

```javascript
class ListNode {
    constructor(val, next) {
        this.val = (val === undefined ? 0 : val);
        this.next = (next === undefined ? null : next);
    }
}
```





## 1. 链表常用操作



### 1. 初始化链表

![](https://www.hello-algo.com/chapter_array_and_linkedlist/linked_list.assets/linkedlist_definition.png)

```javascript
const n0 = new ListNode(1);
const n1 = new ListNode(3);
const n2 = new ListNode(2);
const n3 = new ListNode(5);
const n4 = new ListNode(4);

n0.next = n1;
n1.next = n2;
n2.next = n3;
n3.next = n4;
```

**`数组整体是一个变量，比如数组 nums 包含元素 nums[0] 和 nums[1] 等，而链表是由多个独立的节点对象组成的。我们通常将头节点当作链表的代称，比如以上代码中的链表可记作链表 n0。`**





### 2. 插入节点

![](https://www.hello-algo.com/chapter_array_and_linkedlist/linked_list.assets/linkedlist_insert_node.png)

```javascript
// 在链表的节点 n0 之后插入节点 P

function insert(n0, P) {
    const n1 = n0.next;
    P.next = n1;
    n0.next = P;
}
```





### 3. 删除节点

![](https://www.hello-algo.com/chapter_array_and_linkedlist/linked_list.assets/linkedlist_remove_node.png)

```javascript
// 删除链表的节点 n0 之后的首个节点

function remove(n0) {
    if (!n0.next) return;
    const P = n0.next;
    const n1 = P.next;
    n0.next = n1;
}
```





### 4. 访问节点

**`在链表中访问节点的效率较低。`**

```javascript
// 访问链表中索引为 index 的节点

function access(head, index) {
    for (let i = 0; i < index; i++) {
        if (!head) {
            return null;
        }
        
        head = head.next;
    }
    
    return head;
}
```





### 5. 查找节点

```javascript
// 在链表中查找值为 target 的首个节点

function find(head, target) {
    let index = 0;
    
    while (head !== null) {
        if (head.val === target) {
            return index;
        }
        
        head = head.next;
        index += 1;
    }
    
    return -1;
}
```









```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  // 在链表末尾添加节点
  append(data) {
    const newNode = new Node(data);

    if (!this.head) {
      this.head = newNode;
      return;
    }

    let current = this.head;
    while (current.next) {
      current = current.next;
    }

    current.next = newNode;
  }

  // 打印链表中的所有元素
  printList() {
    let current = this.head;
    let listString = "";

    while (current) {
      listString += current.data + " ";
      current = current.next;
    }

    console.log(listString);
  }
}

// 示例用法
const linkedList = new LinkedList();
linkedList.append(10);
linkedList.append(20);
linkedList.append(30);

linkedList.printList(); // 输出: 10 20 30
```



## 2. 双向链表

```javascript
class DoublyNode {
  constructor(data) {
    this.data = data;
    this.next = null;
    this.prev = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null; // 添加尾指针
  }

  // 在链表末尾添加节点
  append(data) {
    const newNode = new DoublyNode(data);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode; // 同时更新尾指针
      return;
    }

    newNode.prev = this.tail;
    this.tail.next = newNode;
    this.tail = newNode; // 更新尾指针
  }

  // 打印链表中的所有元素 (从头到尾)
  printList() {
    let current = this.head;
    let listString = "";

    while (current) {
      listString += current.data + " ";
      current = current.next;
    }

    console.log(listString);
  }

  // 反向打印链表中的所有元素 (从尾到头)
  printListReverse() {
    let current = this.tail;
    let listString = "";

    while (current) {
      listString += current.data + " ";
      current = current.prev;
    }

    console.log(listString);
  }
}

// 示例用法
const doublyLinkedList = new DoublyLinkedList();
doublyLinkedList.append(10);
doublyLinkedList.append(20);
doublyLinkedList.append(30);

doublyLinkedList.printList(); // 输出: 10 20 30
doublyLinkedList.printListReverse(); // 输出: 30 20 10
```





## 3. 循环链表

```javascript
class CircularNode {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
  }

  // 在链表末尾添加节点
  append(data) {
    const newNode = new CircularNode(data);

    if (!this.head) {
      this.head = newNode;
      newNode.next = this.head; // 循环指向头节点
      return;
    }

    let current = this.head;
    while (current.next !== this.head) { // 找到最后一个节点
      current = current.next;
    }

    current.next = newNode;
    newNode.next = this.head; // 循环指向头节点
  }

  // 打印链表中的所有元素 (循环打印)
  printList(limit = 10) { // 添加一个限制，防止无限循环
    if (!this.head) {
      console.log("Empty list");
      return;
    }

    let current = this.head;
    let listString = "";
    let count = 0;

    do {
      listString += current.data + " ";
      current = current.next;
      count++;

      if (count > limit) { // 限制打印数量
        listString += "...(loop)";
        break;
      }
    } while (current !== this.head);

    console.log(listString);
  }
}

// 示例用法
const circularLinkedList = new CircularLinkedList();
circularLinkedList.append(10);
circularLinkedList.append(20);
circularLinkedList.append(30);

circularLinkedList.printList(); // 输出: 10 20 30 (循环)
```











# 集合





## 1. 构建数据集合

```javascript
class MySet {
  constructor() {
    this.items = {};
  }
}
```





## 2. 创建集合类



### 1. has

```javascript
// 检查元素是否存在
has(element) {
	return this.items.hasOwnProperty(element);
}
```





### 2. add 方法

```javascript
// 添加元素
add(element) {
    if (!this.has(element)) {
      this.items[element] = element;
      return true;
    }
    return false;
}
```





### 3. delete 和 clear 方法

```javascript
// 删除元素
delete(element) {
    if (this.has(element)) {
      delete this.items[element];
      return true;
    }
    return false;
}

// 清空集合
clear() {
	this.items = {};
}
```





### 4. size 方法

```javascript
// 获取集合的大小
size() {
	return Object.keys(this.items).length;
}
```





### 5. values 方法

```javascript
// 获取集合中的所有值 (以数组形式返回)
values() {
	return Object.keys(this.items);
}
```



### 6. 使用 Set 类

```javascript
// 示例用法
const setA = new MySet();
setA.add(1);
setA.add(2);
setA.add(3);

const setB = new MySet();
setB.add(2);
setB.add(3);
setB.add(4);

console.log("Set A values:", setA.values()); // 输出: ["1", "2", "3"]
console.log("Set B values:", setB.values()); // 输出: ["2", "3", "4"]
```





## 3. 集合运算



### 1. 并集

```javascript
// 并集
union(otherSet) {
    const unionSet = new MySet();

    this.values().forEach(value => unionSet.add(value));
    otherSet.values().forEach(value => unionSet.add(value));

    return unionSet;
}
```





### 2. 交集

```javascript
// 交集
intersection(otherSet) {
    const intersectionSet = new MySet();

    this.values().forEach(value => {
      if (otherSet.has(value)) {
        intersectionSet.add(value);
      }
    });

    return intersectionSet;
}
```





### 3. 差集

```javascript
// 差集
difference(otherSet) {
    const differenceSet = new MySet();

    this.values().forEach(value => {
      if (!otherSet.has(value)) {
        differenceSet.add(value);
      }
    });

    return differenceSet;
}
```





### 4. 子集

```javascript
// 子集
isSubsetOf(otherSet) {
    if (this.size() > otherSet.size()) {
    	return false;
    }

    return this.values().every(value => otherSet.has(value));
}
```



```javascript
// 示例用法
const setA = new MySet();
setA.add(1);
setA.add(2);
setA.add(3);

const setB = new MySet();
setB.add(2);
setB.add(3);
setB.add(4);

console.log("Set A values:", setA.values()); // 输出: ["1", "2", "3"]
console.log("Set B values:", setB.values()); // 输出: ["2", "3", "4"]

const unionSet = setA.union(setB);
console.log("Union:", unionSet.values()); // 输出: ["1", "2", "3", "4"]

const intersectionSet = setA.intersection(setB);
console.log("Intersection:", intersectionSet.values()); // 输出: ["2", "3"]

const differenceSet = setA.difference(setB);
console.log("Difference (A - B):", differenceSet.values()); // 输出: ["1"]

console.log("Is A a subset of B?", setA.isSubsetOf(setB)); // 输出: false

const setC = new MySet();
setC.add(2);
setC.add(3);
console.log("Is C a subset of B?", setC.isSubsetOf(setB)); // 输出: true
```







# 字典和散列表



## 1. 字典

```javascript
class Dictionary {
  constructor() {
    this.items = {};
  }

  // 添加键值对
  set(key, value) {
    this.items[key] = value;
  }

  // 删除键值对
  delete(key) {
    if (this.has(key)) {
      delete this.items[key];
      return true;
    }
    return false;
  }

  // 检查键是否存在
  has(key) {
    return this.items.hasOwnProperty(key);
  }

  // 获取值
  get(key) {
    return this.has(key) ? this.items[key] : undefined;
  }

  // 清空字典
  clear() {
    this.items = {};
  }

  // 获取字典的大小
  size() {
    return Object.keys(this.items).length;
  }

  // 获取所有的键
  keys() {
    return Object.keys(this.items);
  }

  // 获取所有的值
  values() {
    return Object.values(this.items);
  }

  // 获取所有的键值对 (以数组形式返回)
  entries() {
    return Object.entries(this.items);
  }
}

// 示例用法
const dictionary = new Dictionary();

dictionary.set("name", "John");
dictionary.set("age", 30);
dictionary.set("city", "New York");

console.log("Name:", dictionary.get("name")); // 输出: John
console.log("Age:", dictionary.get("age")); // 输出: 30
console.log("City:", dictionary.get("city")); // 输出: New York

console.log("Keys:", dictionary.keys()); // 输出: ["name", "age", "city"]
console.log("Values:", dictionary.values()); // 输出: ["John", 30, "New York"]
console.log("Entries:", dictionary.entries()); // 输出: [["name", "John"], ["age", 30], ["city", "New York"]]

dictionary.delete("age");
console.log("Has age?", dictionary.has("age")); // 输出: false
console.log("Size:", dictionary.size()); // 输出: 2
```





## 2. 散列表

```javascript
class HashTable {
  constructor(size = 37) {
    this.table = new Array(size);
    this.size = size;
  }

  // 散列函数 (简单的示例)
  hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % this.size;
  }

  // 添加键值对
  set(key, value) {
    const index = this.hash(key);
    if (!this.table[index]) {
      this.table[index] = [];
    }
    this.table[index].push([key, value]);
  }

  // 获取值
  get(key) {
    const index = this.hash(key);
    if (this.table[index]) {
      for (let i = 0; i < this.table[index].length; i++) {
        if (this.table[index][i][0] === key) {
          return this.table[index][i][1];
        }
      }
    }
    return undefined;
  }

  // 删除键值对
  delete(key) {
    const index = this.hash(key);
    if (this.table[index]) {
      for (let i = 0; i < this.table[index].length; i++) {
        if (this.table[index][i][0] === key) {
          this.table[index].splice(i, 1);
          return true;
        }
      }
    }
    return false;
  }

  // 打印散列表
  display() {
    for (let i = 0; i < this.table.length; i++) {
      if (this.table[i]) {
        console.log(i + ": " + this.table[i].map(item => item[0] + " -> " + item[1]));
      }
    }
  }
}

// 示例用法
const hashTable = new HashTable();

hashTable.set("name", "John");
hashTable.set("age", 30);
hashTable.set("city", "New York");

hashTable.display();
// 可能的输出:
// 10: name -> John
// 30: age -> 30
// 15: city -> New York

console.log("Name:", hashTable.get("name")); // 输出: John
console.log("Age:", hashTable.get("age")); // 输出: 30

hashTable.delete("age");
hashTable.display();
// 可能的输出:
// 10: name -> John
// 15: city -> New York
```











# 递归



## 1. 计算一个数的阶乘

```javascript
function factorial(n) {
    if ( n === 1 || n === 0) {
        return 1;
    }
    
    return n * factorial(n - 1);
}
```





## 2. 计算斐波那契数

```javascript
function fibonacci(n) {
    if (n < 1) return 0;
    if (n <= 2) return 1;
    
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```









# 树



## 1. 二叉树

```javascript
class TreeNode {
    val;
    left;
    right;
    constructor(val, left, right) {
        this.val = val === undefined ? 0 : val;
        this.left = left === undefined ? null : left;
        this.right = right === undefined ? null : right;
    }
}
```



![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/binary_tree_definition.png)

### 1. 二叉树常见术语

* **`根节点（root node）：位于二叉树顶层的节点，没有父节点。`** 
* **`叶节点（leaf node）：没有子节点的节点，其两个指针均指向 none。`** 
* **`边（edge）：连接两个节点的线段，即节点引用（指针）。`** 
* **`节点所在的层（level）：从顶至底递增，根节点所在层为 1。`** 
* **`节点的度（degree）：节点的子节点的数量。在二叉树中，度的取值范围是 0、1、2。`** 
* **`二叉树的高度（height）：从根节点到最远叶节点所经过的边的数量。`** 
* **`节点的深度（depth）：从根节点到该节点所经过的边的数量。`** 
* **`节点的高度（height）：从距离该节点最远的叶节点到该节点所经过的边的数量。`** 

![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/binary_tree_terminology.png)

### 2. 二叉树基本操作



#### 1. 初始化二叉树

**`与链表类似，首先初始化节点，然后构建引用（指针）。`**

```javascript
let n1 = new TreeNode(1),
    n2 = new TreeNode(2),
    n3 = new TreeNode(3),
    n4 = new TreeNode(4),
    n5 = new TreeNode(5);

n1.left = n2;
n1.right = n3;
n2.left = n4;
n2.right = n5;
```



#### 2. 插入与删除节点

**`与链表类似，在二叉树中插入与删除节点可以通过修改指针来实现。如下图给出了一个示例。`** 

![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/binary_tree_add_remove.png)

```javascript
let P = new TreeNode(0);

// 在 n1 -> n2 中间插入节点 P

n1.left = P;
P.left = n2;

// 删除节点 P

n1.left = n2;
```





### 3. 常见二叉树类型



#### 1. 完美二叉树

**`完美二叉树所有层的节点都被完全填满。在完美二叉树中，叶节点的度为 0，其余所有节点的度都为 2。`**

![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/perfect_binary_tree.png)



#### 2. 完全二叉树

**`完全二叉树只有最底层的节点未被填满，且最底层节点尽量靠左填充。请注意，完美二叉树也是一颗完全二叉树。`** 

![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/complete_binary_tree.png)



#### 3. 完满二叉树

**`完满二叉树除了叶节点之外，其余所有节点都有两个子节点。`** 

![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/full_binary_tree.png)

#### 4. 平衡二叉树

**`平衡二叉树中任意节点的左子树和右子树的高度之差的绝对值不超过 1。`**

![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/balanced_binary_tree.png)



### 4. 二叉树的退化

**`如图展示了二叉树的理想结构与退化结构。当二叉树的每层节点都被填满时，达到“完美二叉树”；而当所有节点都偏向一侧时，二叉树退化为“链表”。`** 

- **`完美二叉树是理想情况，可以充分发挥二叉树“分治”的优势。`** 
- **`链表则是另一个极端，各项操作都变为线性操作，时间复杂度退化至 O(n) 。`** 

![](https://www.hello-algo.com/chapter_tree/binary_tree.assets/binary_tree_best_worst_cases.png)



## 2. 二叉树遍历



### 1. 层序遍历

**`层序遍历从顶部到底部逐层遍历二叉树，并在每一层按照从左到右的顺序访问节点。`**

**`层序遍历本质上属于广度优先遍历，也称广度优先搜索，它体现了一种一圈一圈向外扩展的逐层遍历方式。`**

![](https://www.hello-algo.com/chapter_tree/binary_tree_traversal.assets/binary_tree_bfs.png)

#### 1. 代码实现

**`广度优先遍历通常借助队列来实现。队列遵循先进先出的规则，而广度优先遍历则遵循逐层推进的规则，两者背后的思想是一致的。实现代码如下：`** 

```javascript
function levelOrder(root) {
    const queue = [root];
    const list = [];
    while (queue.length) {
        let node = queue.shift();
        list.push(node.val);
        if (node.left) queue.push(node.left);
        if (node.right) queue.push(node.right);
    }
    
    return list;
}
```





### 2. 前序、中序、后序遍历

**`相应地，前序、中序和后序遍历都属于深度优先遍历，也称深度优先搜索，它体现了一种先走到尽头，再回溯继续的遍历方式。`**

**`如图展示了对二叉树进行深度优先遍历的工作原理。深度优先遍历就像是绕着整棵二叉树的外围走一圈，在每个节点都会遇到三个位置，分别对应前序遍历、中序遍历和后序遍历。`**

![](https://www.hello-algo.com/chapter_tree/binary_tree_traversal.assets/binary_tree_dfs.png)



#### 1. 代码实现

**`深度优先搜索通常基于递归实现：`**

```javascript
// 前序遍历
function preOrder(root) {
    if (root === null) return;
    
    // 访问优先级：根节点 -> 左子树 -> 右子树
    list.push(root.val);
    preOrder(root.left);
    preOrder(root.right);
}


// 中序遍历
function inOrder(root) {
    if (root === null) return;
    
    // 访问优先级：左子树 -> 根节点 -> 右子树
    inOrder(root.left);
    list.push(root.val);
    inOrder(root.right);
}


// 后序遍历
function postOrder(root) {
    if (root === null) return;
    
    // 访问优先级：左子树 -> 右子树 -> 根节点
    postOrder(root.left);
    postOrder(root.right);
    list.push(root.val);
}
```





## 3. 二叉树数组表示









## 4. 二叉搜索树

如图所示，二叉搜索树满足以下条件。

1. 对于根节点，左子树中所有节点的值 < 根节点的值 < 右子树中所有节点的值。
2. 任意节点的左、右子树也是二叉搜索树，即同样满足条件 1。

![](https://www.hello-algo.com/chapter_tree/binary_search_tree.assets/binary_search_tree.png)

### 1. 二叉搜索树的操作



#### 1. 查找节点

```javascript
search(num) {
    let cur = this.root;
    while (cur !== null) {
        if (cur.val < num) cur = cur.right;
        else if (cur.val > num) cur = cur.left;
        else break;
    }
    
    return cur;
}
```





#### 2. 插入节点

```javascript
insert(num) {
    if (this.root === null) {
        this.root = new TreeNode(num);
        return;
    }
    
    let cur = this.root,
        pre = null;
    while (cur !== null) {
        if (cur.val === num) return;
        pre = cur;
        if (cur.val < num) cur = cur.right;
        else cur = cur.left;
    }
    
    const node = new TreeNode(num);
    if (pre.val < num) pre.right = node;
    else pre.left = node;
}
```



#### 



# 图

```javascript
class Graph {
  constructor(isDirected = false) {
    this.isDirected = isDirected; // 是否是有向图
    this.adjacencyList = new Map(); // 邻接表
  }

  // 添加顶点
  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, []);
    }
  }

  // 添加边
  addEdge(vertex1, vertex2, weight = 0) {
    if (!this.adjacencyList.has(vertex1) || !this.adjacencyList.has(vertex2)) {
      console.log("顶点不存在");
      return;
    }

    this.adjacencyList.get(vertex1).push({ vertex: vertex2, weight: weight });

    if (!this.isDirected) {
      this.adjacencyList.get(vertex2).push({ vertex: vertex1, weight: weight });
    }
  }

  // 获取顶点的邻居
  getNeighbors(vertex) {
    return this.adjacencyList.get(vertex) || [];
  }

  // 获取所有的顶点
  getVertices() {
    return Array.from(this.adjacencyList.keys());
  }

  // 打印图
  printGraph() {
    for (let [vertex, edges] of this.adjacencyList) {
      let neighbors = edges.map(edge => `${edge.vertex}(${edge.weight})`).join(", ");
      console.log(`${vertex} -> ${neighbors}`);
    }
  }
}
```





## 1. 图的遍历



### 1. 广度优先搜索

```javascript
// 广度优先搜索 (BFS)
function bfs(graph, startVertex, callback) {
  const visited = new Set();
  const queue = [startVertex];

  visited.add(startVertex);

  while (queue.length > 0) {
    const vertex = queue.shift();
    callback(vertex); // 执行回调函数

    const neighbors = graph.getNeighbors(vertex);
    for (let neighbor of neighbors) {
      if (!visited.has(neighbor.vertex)) {
        visited.add(neighbor.vertex);
        queue.push(neighbor.vertex);
      }
    }
  }
}
```





### 2. 深度优先搜索

```javascript
// 深度优先搜索 (DFS)
function dfs(graph, startVertex, callback) {
  const visited = new Set();

  function dfsHelper(vertex) {
    visited.add(vertex);
    callback(vertex); // 执行回调函数

    const neighbors = graph.getNeighbors(vertex);
    for (let neighbor of neighbors) {
      if (!visited.has(neighbor.vertex)) {
        dfsHelper(neighbor.vertex);
      }
    }
  }

  dfsHelper(startVertex);
}
```





## 2. 最短路径算法



### 1. Dijkstra 算法

```javascript
function dijkstra(graph, startVertex) {
  const distances = {}; // 存储从 startVertex 到每个顶点的最短距离
  const visited = new Set(); // 存储已访问的顶点
  const previous = {}; // 存储每个顶点的前一个顶点，用于重建最短路径

  // 初始化距离
  const vertices = graph.getVertices();
  for (let vertex of vertices) {
    distances[vertex] = Infinity; // 初始距离设置为无穷大
    previous[vertex] = null; // 初始前一个顶点设置为 null
  }
  distances[startVertex] = 0; // startVertex 到自身的距离为 0

  while (true) {
    // 找到当前距离 startVertex 最近的未访问顶点
    let closestVertex = null;
    let closestDistance = Infinity;
    for (let vertex of vertices) {
      if (!visited.has(vertex) && distances[vertex] < closestDistance) {
        closestVertex = vertex;
        closestDistance = distances[vertex];
      }
    }

    // 如果找不到未访问顶点，则算法结束
    if (closestVertex === null) {
      break;
    }

    visited.add(closestVertex); // 标记为已访问

    // 更新邻居的距离
    const neighbors = graph.getNeighbors(closestVertex);
    for (let neighbor of neighbors) {
      const distance = distances[closestVertex] + neighbor.weight;
      if (distance < distances[neighbor.vertex]) {
        distances[neighbor.vertex] = distance;
        previous[neighbor.vertex] = closestVertex;
      }
    }
  }

  return { distances, previous };
}

// 重建最短路径
function reconstructPath(startVertex, endVertex, previous) {
  const path = [];
  let currentVertex = endVertex;

  while (currentVertex !== null) {
    path.unshift(currentVertex);
    currentVertex = previous[currentVertex];
  }

  if (path[0] === startVertex) {
    return path;
  } else {
    return []; // 没有找到路径
  }
}
```



### 2. Floyd-Warshall 算法

```javascript
function floydWarshall(graph) {
  const vertices = graph.getVertices();
  const numVertices = vertices.length;

  // 初始化距离矩阵
  const distances = {};
  for (let i = 0; i < numVertices; i++) {
    distances[vertices[i]] = {};
    for (let j = 0; j < numVertices; j++) {
      if (i === j) {
        distances[vertices[i]][vertices[j]] = 0; // 对角线为 0
      } else {
        distances[vertices[i]][vertices[j]] = Infinity; // 初始距离设置为无穷大
      }
    }
  }

  // 添加已知的边
  for (let vertex of vertices) {
    const neighbors = graph.getNeighbors(vertex);
    for (let neighbor of neighbors) {
      distances[vertex][neighbor.vertex] = neighbor.weight;
    }
  }

  // Floyd-Warshall 算法核心
  for (let k = 0; k < numVertices; k++) {
    for (let i = 0; i < numVertices; i++) {
      for (let j = 0; j < numVertices; j++) {
        if (distances[vertices[i]][vertices[k]] + distances[vertices[k]][vertices[j]] < distances[vertices[i]][vertices[j]]) {
          distances[vertices[i]][vertices[j]] = distances[vertices[i]][vertices[k]] + distances[vertices[k]][vertices[j]];
        }
      }
    }
  }

  return distances;
}
```





## 3. 最小生成树



### 1. Prim 算法

```javascript
function prim(graph, startVertex) {
  const mst = new Set(); // 存储最小生成树中的顶点
  const edges = []; // 存储连接最小生成树和剩余顶点的边
  const visited = new Set(); // 存储已访问的顶点

  mst.add(startVertex);
  visited.add(startVertex);

  // 将与 startVertex 相邻的边添加到 edges 数组中
  const neighbors = graph.getNeighbors(startVertex);
  for (let neighbor of neighbors) {
    edges.push({ from: startVertex, to: neighbor.vertex, weight: neighbor.weight });
  }

  while (mst.size < graph.getVertices().length) {
    // 找到权重最小的边
    let minEdge = null;
    let minWeight = Infinity;
    let minIndex = -1;
    for (let i = 0; i < edges.length; i++) {
      if (edges[i].weight < minWeight) {
        minWeight = edges[i].weight;
        minEdge = edges[i];
        minIndex = i;
      }
    }

    // 如果找不到边，则算法结束
    if (minEdge === null) {
      break;
    }

    // 将权重最小的边添加到最小生成树中
    if (!visited.has(minEdge.to)) {
      mst.add(minEdge.to);
      visited.add(minEdge.to);

      // 将与新顶点相邻的边添加到 edges 数组中
      const newNeighbors = graph.getNeighbors(minEdge.to);
      for (let neighbor of newNeighbors) {
        if (!visited.has(neighbor.vertex)) {
          edges.push({ from: minEdge.to, to: neighbor.vertex, weight: neighbor.weight });
        }
      }
    }

    edges.splice(minIndex, 1); // 从 edges 数组中删除该边
  }

  return mst;
}
```





### 2. Kruskal 算法

```javascript
// 并查集数据结构
class DisjointSet {
  constructor(vertices) {
    this.parent = {};
    for (let vertex of vertices) {
      this.parent[vertex] = vertex; // 初始时，每个顶点的父节点都是自身
    }
  }

  // 查找顶点的根节点
  find(vertex) {
    if (this.parent[vertex] === vertex) {
      return vertex;
    }
    return this.find(this.parent[vertex]); // 路径压缩
  }

  // 合并两个集合
  union(vertex1, vertex2) {
    const root1 = this.find(vertex1);
    const root2 = this.find(vertex2);
    this.parent[root1] = root2;
  }
}

function kruskal(graph) {
  const mst = new Set(); // 存储最小生成树中的边
  const edges = []; // 存储所有的边
  const vertices = graph.getVertices();

  // 将所有的边添加到 edges 数组中
  for (let vertex of vertices) {
    const neighbors = graph.getNeighbors(vertex);
    for (let neighbor of neighbors) {
      edges.push({ from: vertex, to: neighbor.vertex, weight: neighbor.weight });
    }
  }

  // 对边按照权重进行排序
  edges.sort((a, b) => a.weight - b.weight);

  // 使用并查集来判断是否形成环
  const disjointSet = new DisjointSet(vertices);

  for (let edge of edges) {
    const root1 = disjointSet.find(edge.from);
    const root2 = disjointSet.find(edge.to);

    // 如果两个顶点不在同一个集合中，则将该边添加到最小生成树中
    if (root1 !== root2) {
      mst.add(edge);
      disjointSet.union(edge.from, edge.to);
    }
  }

  return mst;
}
```







# 排序和搜索算法



## 1. 冒泡算法

```                                                                                                                                                                                                                                                                                                                                                                                                                                javascript
function bubbleSort(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr.length - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
        }
    }
    
    return arr;
}
```





## 2. 选择排序

```javascript
function selectionSort(arr) {
    for(let i = 0; i < arr.length - 1; i++) {
        let minIndex = i;
        
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        
        if (minIndex !== i) {
            [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
        }
    }
    
    return arr;
}
```





## 3. 插入排序

```javascript
function insertionSort(arr) {
    for (let i = 1; i < arr.length; i++) {
        let key = arr[i];
        let j = i - 1;
        
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        
        arr[j + 1] = key;
    }
    
    return arr;
}
```





## 4. 归并排序

```javascript
function mergeSort(arr) {
    if (arr.length <= 1) {
        return arr;
    }
    
    const mid = Math.floor(arr.length / 2);
    const left = arr.slice(0, mid);
    const right = arr.slice(mid);
    
    return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
    let result = [];
    let leftIndex = 0;
    let rightIndex = 0;
    
    while (leftIndex < left.length && rightIndex < right.length) {
        if (left[leftIndex] < right[rightIndex]) {
            result.push(left[leftIndex]);
            leftIndex++;
        } else {
            result.push(right[rightIndex]);
            rightIndex++;
        }
    }
    
    return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}
```







## 5. 快速排序

```javascript
function partition(nums, left, right) {
    let i = left, j= right;
    while(i < j) {
        while(i < j && nums[j] >= nums[left]) {
            j -= 1;
        }
        
        while(i < j && nums[i] <= nums[left]) {
            i += 1;
        }
        
        [nums[i], nums[j]] = [nums[j], nums[i]];
    }
    
    [nums[i], nums[left]] = [nums[left], nums[i]];
    
    return i;
}


function quickSort(nums, left, right) {
    while (left < right) {
        // 1. 划分数组
        const pivotIndex = partition(nums, left, right);
        // 2. 递归排序左子数组
        quickSort(nums, left, pivotIndex - 1);
        // 3. 递归排序右子数组
        quickSort(nums, pivotIndex + 1, right);
    }
}
```





## 6. 堆排序

```javascript
/* 堆的长度为 n ，从节点 i 开始，从顶至底堆化 */
function siftDown(nums, n, i) {
    while (true) {
        // 判断节点 i, l, r 中值最大的节点，记为 ma
        let l = 2 * i + 1;
        let r = 2 * i + 2;
        let ma = i;
        if (l < n && nums[l] > nums[ma]) {
            ma = l;
        }
        if (r < n && nums[r] > nums[ma]) {
            ma = r;
        }
        // 若节点 i 最大或索引 l, r 越界，则无须继续堆化，跳出
        if (ma === i) {
            break;
        }
        // 交换两节点
        [nums[i], nums[ma]] = [nums[ma], nums[i]];
        // 循环向下堆化
        i = ma;
    }
}

/* 堆排序 */
function heapSort(nums) {
    // 建堆操作：堆化除叶节点以外的其他所有节点
    for (let i = Math.floor(nums.length / 2) - 1; i >= 0; i--) {
        siftDown(nums, nums.length, i);
    }
    // 从堆中提取最大元素，循环 n-1 轮
    for (let i = nums.length - 1; i > 0; i--) {
        // 交换根节点与最右叶节点（交换首元素与尾元素）
        [nums[0], nums[i]] = [nums[i], nums[0]];
        // 以根节点为起点，从顶至底进行堆化
        siftDown(nums, i, 0);
    }
}
```





## 7. 桶排序

```javascript
/* 桶排序 */
function bucketSort(nums) {
    // 初始化 k = n/2 个桶，预期向每个桶分配 2 个元素
    const k = nums.length / 2;
    const buckets = [];
    for (let i = 0; i < k; i++) {
        buckets.push([]);
    }
    // 1. 将数组元素分配到各个桶中
    for (const num of nums) {
        // 输入数据范围为 [0, 1)，使用 num * k 映射到索引范围 [0, k-1]
        const i = Math.floor(num * k);
        // 将 num 添加进桶 i
        buckets[i].push(num);
    }
    // 2. 对各个桶执行排序
    for (const bucket of buckets) {
        // 使用内置排序函数，也可以替换成其他排序算法
        bucket.sort((a, b) => a - b);
    }
    // 3. 遍历桶合并结果
    let i = 0;
    for (const bucket of buckets) {
        for (const num of bucket) {
            nums[i++] = num;
        }
    }
}
```







## 8. 计数排序

```javascript
/* 计数排序 */
// 完整实现，可排序对象，并且是稳定排序
function countingSort(nums) {
    // 1. 统计数组最大元素 m
    let m = 0;
    for (const num of nums) {
        m = Math.max(m, num);
    }
    // 2. 统计各数字的出现次数
    // counter[num] 代表 num 的出现次数
    const counter = new Array(m + 1).fill(0);
    for (const num of nums) {
        counter[num]++;
    }
    // 3. 求 counter 的前缀和，将“出现次数”转换为“尾索引”
    // 即 counter[num]-1 是 num 在 res 中最后一次出现的索引
    for (let i = 0; i < m; i++) {
        counter[i + 1] += counter[i];
    }
    // 4. 倒序遍历 nums ，将各元素填入结果数组 res
    // 初始化数组 res 用于记录结果
    const n = nums.length;
    const res = new Array(n);
    for (let i = n - 1; i >= 0; i--) {
        const num = nums[i];
        res[counter[num] - 1] = num; // 将 num 放置到对应索引处
        counter[num]--; // 令前缀和自减 1 ，得到下次放置 num 的索引
    }
    // 使用结果数组 res 覆盖原数组 nums
    for (let i = 0; i < n; i++) {
        nums[i] = res[i];
    }
}
```





## 9. 基数排序

```javascript
/* 获取元素 num 的第 k 位，其中 exp = 10^(k-1) */
function digit(num, exp) {
    // 传入 exp 而非 k 可以避免在此重复执行昂贵的次方计算
    return Math.floor(num / exp) % 10;
}

/* 计数排序（根据 nums 第 k 位排序） */
function countingSortDigit(nums, exp) {
    // 十进制的位范围为 0~9 ，因此需要长度为 10 的桶数组
    const counter = new Array(10).fill(0);
    const n = nums.length;
    // 统计 0~9 各数字的出现次数
    for (let i = 0; i < n; i++) {
        const d = digit(nums[i], exp); // 获取 nums[i] 第 k 位，记为 d
        counter[d]++; // 统计数字 d 的出现次数
    }
    // 求前缀和，将“出现个数”转换为“数组索引”
    for (let i = 1; i < 10; i++) {
        counter[i] += counter[i - 1];
    }
    // 倒序遍历，根据桶内统计结果，将各元素填入 res
    const res = new Array(n).fill(0);
    for (let i = n - 1; i >= 0; i--) {
        const d = digit(nums[i], exp);
        const j = counter[d] - 1; // 获取 d 在数组中的索引 j
        res[j] = nums[i]; // 将当前元素填入索引 j
        counter[d]--; // 将 d 的数量减 1
    }
    // 使用结果覆盖原数组 nums
    for (let i = 0; i < n; i++) {
        nums[i] = res[i];
    }
}

/* 基数排序 */
function radixSort(nums) {
    // 获取数组的最大元素，用于判断最大位数
    let m = Number.MIN_VALUE;
    for (const num of nums) {
        if (num > m) {
            m = num;
        }
    }
    // 按照从低位到高位的顺序遍历
    for (let exp = 1; exp <= m; exp *= 10) {
        // 对数组元素的第 k 位执行计数排序
        // k = 1 -> exp = 1
        // k = 2 -> exp = 10
        // 即 exp = 10^(k-1)
        countingSortDigit(nums, exp);
    }
}
```



