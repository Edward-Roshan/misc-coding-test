# misc-coding-test
一些杂乱无章，但又有点意思的代码测试

## 1.用setTimeout模拟setInterval

```javascirpt
function mockRequest() {
  return new Promise((resolve) => {
    globalThis.setTimeout(() => {
      resolve();
    }, 1000);
  });
}

function mockInterval(func, interval) {
  function fn(){
    func();
    console.log(new Date());
    setTimeout(fn, interval);
  }
  setTimeout(fn, interval);
}

mockInterval(mockRequest, 3000);
```

## 2.反转双向链表

```javascript

let head = null;
let tail = null;

class Node {
  constructor(value) {
    this.value = value;
    this.prev = null;
    this.next = null;
  }
}

const createNode = (value) => {
  const node = new Node(value);
  node.prev = null;
  node.next = head;
  
  if(head != null) {
    head.prev = node;
  }
  
  head = node;
}


const display = (node) => {
  while(node != null) {
    console.log(node.value);
    node = node.next;
  }
}

const reverse = () => {
  let temp = null;
  let current = head;
  while(current != null) {
    temp = current.prev;
    current.prev = current.next;
    current.next = temp;
    current = current.prev;
  }
  
  if(temp != null)
    head = temp.prev;
}

createNode(5);
createNode(4);
createNode(3);
createNode(2);
createNode(1);

display(head);

reverse();
display(head);
```

## 3.Redux的Compose函数

```javascript
function compose(...funcs) {
    if (funcs.length === 0) {
        return arg => arg
    }
 
    if (funcs.length === 1) {
        return funcs[0]
    }
 
    return funcs.reduce((a, b) => (...args) => a(b(...args)))
} 
```
