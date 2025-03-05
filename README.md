

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



## 1. 双向链表

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





## 2. 循环链表

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



## 1. 树数据结构

**`首先，我们定义一个简单的树节点类：`**

```javascript
class TreeNode {
    constructor(val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}
```





## 2. 二叉搜索树（BST）

```javascript
class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  // 插入节点
  insert(val) {
    const newNode = new TreeNode(val);

    if (!this.root) {
      this.root = newNode;
      return;
    }

    this.insertNode(this.root, newNode);
  }

  insertNode(node, newNode) {
    if (newNode.val < node.val) {
      if (!node.left) {
        node.left = newNode;
      } else {
        this.insertNode(node.left, newNode);
      }
    } else {
      if (!node.right) {
        node.right = newNode;
      } else {
        this.insertNode(node.right, newNode);
      }
    }
  }

  // 搜索最小值
  min() {
    if (!this.root) {
      return null;
    }
    return this.minNode(this.root).val;
  }

  minNode(node) {
    let current = node;
    while (current && current.left) {
      current = current.left;
    }
    return current;
  }

  // 搜索最大值
  max() {
    if (!this.root) {
      return null;
    }
    return this.maxNode(this.root).val;
  }

  maxNode(node) {
    let current = node;
    while (current && current.right) {
      current = current.right;
    }
    return current;
  }

  // 搜索特定值
  search(val) {
    return this.searchNode(this.root, val);
  }

  searchNode(node, val) {
    if (!node) {
      return false;
    }

    if (val < node.val) {
      return this.searchNode(node.left, val);
    } else if (val > node.val) {
      return this.searchNode(node.right, val);
    } else {
      return true;
    }
  }

  // 移除节点
  remove(val) {
    this.root = this.removeNode(this.root, val);
  }

  removeNode(node, val) {
    if (!node) {
      return null;
    }

    if (val < node.val) {
      node.left = this.removeNode(node.left, val);
      return node;
    } else if (val > node.val) {
      node.right = this.removeNode(node.right, val);
      return node;
    } else {
      // 找到要删除的节点

      // 情况 1: 叶子节点
      if (!node.left && !node.right) {
        node = null;
        return node;
      }

      // 情况 2: 只有一个子节点
      if (!node.left) {
        node = node.right;
        return node;
      } else if (!node.right) {
        node = node.left;
        return node;
      }

      // 情况 3: 有两个子节点
      const aux = this.minNode(node.right); // 找到右子树的最小值
      node.val = aux.val; // 将右子树的最小值替换当前节点的值
      node.right = this.removeNode(node.right, aux.val); // 从右子树中移除最小值
      return node;
    }
  }

  // 中序遍历
  inorderTraversal(callback) {
    this.inorderTraversalNode(this.root, callback);
  }

  inorderTraversalNode(node, callback) {
    if (node) {
      this.inorderTraversalNode(node.left, callback);
      callback(node.val);
      this.inorderTraversalNode(node.right, callback);
    }
  }
}
```









## 3. 树的遍历



### 1. 先序遍历

* **`递归实现`**

```javascript
function preorderTraversalRecursive(root) {
  const result = [];

  function traverse(node) {
    if (node) {
      result.push(node.val); // 访问根节点
      traverse(node.left);   // 遍历左子树
      traverse(node.right);  // 遍历右子树
    }
  }

  traverse(root);
  return result;
}
```



* **`迭代实现`**

```javascript
function preorderTraversalIterative(root) {
  const result = [];
  const stack = [];

  if (root) {
    stack.push(root);
  }

  while (stack.length > 0) {
    const node = stack.pop();
    result.push(node.val);

    // 先将右子节点入栈，因为栈是后进先出
    if (node.right) {
      stack.push(node.right);
    }
    if (node.left) {
      stack.push(node.left);
    }
  }

  return result;
}
```



### 2. 中序遍历

* **`递归实现：`**

```javascript
function inorderTraversalRecursive(root) {
  const result = [];

  function traverse(node) {
    if (node) {
      traverse(node.left);   // 遍历左子树
      result.push(node.val); // 访问根节点
      traverse(node.right);  // 遍历右子树
    }
  }

  traverse(root);
  return result;
}
```



* **`迭代实现：`**

```javascript
function inorderTraversalIterative(root) {
  const result = [];
  const stack = [];
  let current = root;

  while (current || stack.length > 0) {
    // 将所有左子节点入栈
    while (current) {
      stack.push(current);
      current = current.left;
    }

    // 访问栈顶节点
    current = stack.pop();
    result.push(current.val);

    // 遍历右子树
    current = current.right;
  }

  return result;
}
```



### 3. 后序遍历

* **`递归实现：`**

```javascript
function postorderTraversalRecursive(root) {
  const result = [];

  function traverse(node) {
    if (node) {
      traverse(node.left);   // 遍历左子树
      traverse(node.right);  // 遍历右子树
      result.push(node.val); // 访问根节点
    }
  }

  traverse(root);
  return result;
}
```



* **`迭代实现：`**

```javascript
function postorderTraversalIterative(root) {
  const result = [];
  const stack = [];
  let lastVisited = null;
  let current = root;

  while (current || stack.length > 0) {
    // 将所有左子节点入栈
    while (current) {
      stack.push(current);
      current = current.left;
    }

    // 查看栈顶节点
    current = stack[stack.length - 1];

    // 如果右子节点存在且未被访问过，则遍历右子树
    if (current.right && lastVisited !== current.right) {
      current = current.right;
    } else {
      // 访问栈顶节点
      result.push(current.val);
      lastVisited = stack.pop();
      current = null; // 访问完节点后，将 current 设置为 null
    }
  }

  return result;
}
```





## 4. 自平衡树



### 1. AVL 树

```javascript
class AVLTreeNode extends TreeNode {
  constructor(val) {
    super(val);
    this.height = 1; // 新节点的初始高度为 1
  }
}

class AVLTree extends BinarySearchTree {
  constructor() {
    super();
  }

  // 获取节点的高度
  getHeight(node) {
    if (!node) {
      return 0;
    }
    return node.height;
  }

  // 右旋
  rightRotate(y) {
    const x = y.left;
    const T2 = x.right;

    // 执行旋转
    x.right = y;
    y.left = T2;

    // 更新高度
    y.height = Math.max(this.getHeight(y.left), this.getHeight(y.right)) + 1;
    x.height = Math.max(this.getHeight(x.left), this.getHeight(x.right)) + 1;

    return x; // 返回新的根节点
  }

  // 左旋
  leftRotate(x) {
    const y = x.right;
    const T2 = y.left;

    // 执行旋转
    y.left = x;
    x.right = T2;

    // 更新高度
    x.height = Math.max(this.getHeight(x.left), this.getHeight(x.right)) + 1;
    y.height = Math.max(this.getHeight(y.left), this.getHeight(y.right)) + 1;

    return y; // 返回新的根节点
  }

  // 获取平衡因子
  getBalanceFactor(node) {
    if (!node) {
      return 0;
    }
    return this.getHeight(node.left) - this.getHeight(node.right);
  }

  // 插入节点 (AVL 树版本)
  insert(val) {
    const newNode = new AVLTreeNode(val);
    this.root = this.insertNode(this.root, newNode);
  }

  insertNode(node, newNode) {
    if (!node) {
      return newNode;
    }

    if (newNode.val < node.val) {
      node.left = this.insertNode(node.left, newNode);
    } else if (newNode.val > node.val) {
      node.right = this.insertNode(node.right, newNode);
    } else {
      return node; // 不允许重复值
    }

    // 更新当前节点的高度
    node.height = Math.max(this.getHeight(node.left), this.getHeight(node.right)) + 1;

    // 获取平衡因子
    const balanceFactor = this.getBalanceFactor(node);

    // 执行旋转以保持平衡
    if (balanceFactor > 1 && newNode.val < node.left.val) {
      // 左-左 情况
      return this.rightRotate(node);
    }

    if (balanceFactor < -1 && newNode.val > node.right.val) {
      // 右-右 情况
      return this.leftRotate(node);
    }

    if (balanceFactor > 1 && newNode.val > node.left.val) {
      // 左-右 情况
      node.left = this.leftRotate(node.left);
      return this.rightRotate(node);
    }

    if (balanceFactor < -1 && newNode.val < node.right.val) {
      // 右-左 情况
      node.right = this.rightRotate(node.right);
      return this.leftRotate(node);
    }

    return node;
  }

  // 移除节点 (AVL 树版本)
  remove(val) {
    this.root = this.removeNode(this.root, val);
  }

  removeNode(node, val) {
    if (!node) {
      return null;
    }

    if (val < node.val) {
      node.left = this.removeNode(node.left, val);
    } else if (val > node.val) {
      node.right = this.removeNode(node.right, val);
    } else {
      // 找到要删除的节点

      // 情况 1: 叶子节点
      if (!node.left && !node.right) {
        return null;
      }

      // 情况 2: 只有一个子节点
      if (!node.left) {
        return node.right;
      } else if (!node.right) {
        return node.left;
      }

      // 情况 3: 有两个子节点
      const aux = this.minNode(node.right);
      node.val = aux.val;
      node.right = this.removeNode(node.right, aux.val);
    }

    if (!node) {
      return null;
    }

    // 更新当前节点的高度
    node.height = Math.max(this.getHeight(node.left), this.getHeight(node.right)) + 1;

    // 获取平衡因子
    const balanceFactor = this.getBalanceFactor(node);

    // 执行旋转以保持平衡
    if (balanceFactor > 1 && this.getBalanceFactor(node.left) >= 0) {
      // 左-左 情况
      return this.rightRotate(node);
    }

    if (balanceFactor < -1 && this.getBalanceFactor(node.right) <= 0) {
      // 右-右 情况
      return this.leftRotate(node);
    }

    if (balanceFactor > 1 && this.getBalanceFactor(node.left) < 0) {
      // 左-右 情况
      node.left = this.leftRotate(node.left);
      return this.rightRotate(node);
    }

    if (balanceFactor < -1 && this.getBalanceFactor(node.right) > 0) {
      // 右-左 情况
      node.right = this.rightRotate(node.right);
      return this.leftRotate(node);
    }

    return node;
  }
}
```







### 2. 红黑树

```javascript
const RED = "RED";
const BLACK = "BLACK";

class RedBlackTreeNode {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
    this.color = RED; // 新节点默认为红色
  }
}

class RedBlackTree {
  constructor() {
    this.root = null;
  }

  // 左旋
  leftRotate(node) {
    const y = node.right;
    node.right = y.left;
    if (y.left) {
      y.left.parent = node;
    }
    y.parent = node.parent;
    if (!node.parent) {
      this.root = y;
    } else if (node === node.parent.left) {
      node.parent.left = y;
    } else {
      node.parent.right = y;
    }
    y.left = node;
    node.parent = y;
  }

  // 右旋
  rightRotate(node) {
    const x = node.left;
    node.left = x.right;
    if (x.right) {
      x.right.parent = node;
    }
    x.parent = node.parent;
    if (!node.parent) {
      this.root = x;
    } else if (node === node.parent.left) {
      node.parent.left = x;
    } else {
      node.parent.right = x;
    }
    x.right = node;
    node.parent = x;
  }

  // 颜色翻转
  flipColors(node) {
    node.color = RED;
    node.left.color = BLACK;
    node.right.color = BLACK;
  }

  // 插入节点
  insert(val) {
    const newNode = new RedBlackTreeNode(val);
    this.root = this.insertNode(this.root, newNode);
    this.root.color = BLACK; // 根节点始终为黑色
  }

  insertNode(node, newNode) {
    if (!node) {
      return newNode;
    }

    if (newNode.val < node.val) {
      node.left = this.insertNode(node.left, newNode);
      node.left.parent = node;
    } else if (newNode.val > node.val) {
      node.right = this.insertNode(node.right, newNode);
      node.right.parent = node;
    } else {
      return node; // 不允许重复值
    }

    // 维护红黑树的性质
    if (this.isRed(node.right) && !this.isRed(node.left)) {
      node = this.leftRotate(node);
    }
    if (this.isRed(node.left) && this.isRed(node.left.left)) {
      node = this.rightRotate(node);
    }
    if (this.isRed(node.left) && this.isRed(node.right)) {
      this.flipColors(node);
    }

    return node;
  }

  // 判断节点是否为红色
  isRed(node) {
    if (!node) {
      return false; // 空节点默认为黑色
    }
    return node.color === RED;
  }

  // 中序遍历
  inorderTraversal(callback) {
    this.inorderTraversalNode(this.root, callback);
  }

  inorderTraversalNode(node, callback) {
    if (node) {
      this.inorderTraversalNode(node.left, callback);
      callback(node.val, node.color);
      this.inorderTraversalNode(node.right, callback);
    }
  }
}
```











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

