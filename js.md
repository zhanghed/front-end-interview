# javascript

## api

### 获取 DOM 对象

```html
<div class="box">
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
  </ul>
</div>
<script>
  // 1. document.querySelector() 选择指定css选择器的第一个元素
  // 1.1 参数是字符串的css选择器
  const box = document.querySelector("div");
  console.log(box);
  console.dir(box);
  const box = document.querySelector(".box");
  console.log(box);
  const li = document.querySelector("ul li");
  console.log(li);
  const li = document.querySelector("ul li:nth-child(2)");
  console.log(li);

  // 2. document.querySelectorAll() 选择指定css选择器的所有元素
  // 2.1 参数还是字符串的css选择器
  const lis = document.querySelectorAll("ul li:nth-child(2n+1)");
  console.log(lis); // 返回值是一个伪数组里面包含了所有的dom对象 li
</script>
```

### 操作元素

```html
<style>
  .black {
    border: 2px solid black;
  }
</style>
<div class="box" data-name="1">
  <img src="" alt="123" />
</div>
<script>
  // 操作元素内容
  // 1. 对象.innerText 文本中包含的标签不会会被解析
  const box = document.querySelector(".box");
  box.innerText = "佟丽丫丫";

  // 2. 对象.innerHTML  文本中包含的标签会被解析。
  box.innerHTML = "<strong>迪丽热巴</strong>";

  // 操作元素属性
  // 1. 直接通过过属性名修改，最简洁的语法
  const img = document.querySelector("img");
  img.alt = "没有图片";

  // 2. 通过style操作元素样式
  const box = document.querySelector(".box");
  box.style.width = "300px";
  box.style.marginTop = "50px";
  box.style.backgroundColor = "pink";

  // 3. 利用类名操作元素样式 利用类名操作样式添加的新的类名会覆盖掉原先的类名
  box.className = "box black";

  // 4. 通过classList操作元素样式(推荐)
  // 4.1 追加类名
  box.classList.add("black");
  // 4.2 删除类名
  box.classList.remove("black");
  // 4.3 切换类名： 如果元素身上有这个类名，那么就删除，如果没有这个类名则添加
  box.classList.toggle("black");

  // 5. 定义属性
  console.log(box.dataset); // 得到一个对象集合
  box.dataset.name = "2";
  console.log(box.dataset);
</script>
```

### 事件

事件监听

```html
<body>
  <div class="box">按钮</div>
  <span>输入框：</span><input type="text" class="search" value="" />
  <script>
    const box = document.querySelector(".box");
    const search = document.querySelector(".search");
    const span = document.querySelector("span");

    // 鼠标事件
    box.addEventListener("click", function () {
      console.log("我点击了盒子");
    });
    box.addEventListener("mouseenter", function () {
      console.log("我鼠标经过了盒子");
    });
    box.addEventListener("mouseleave", function () {
      console.log("我鼠标离开了盒子");
    });

    // 焦点事件(手动触发)
    search.addEventListener("focus", function () {
      console.log("获得了焦点");
    });
    search.addEventListener("blur", function () {
      console.log("失去了焦点");
    });

    // 键盘事件
    search.addEventListener("keydown", function () {
      console.log("我是keydown事件" + search.value);
    });
    search.addEventListener("keyup", function () {
      console.log("我是keyup事件" + search.value);
    });
    search.addEventListener("input", function () {
      console.log("我是input事件" + search.value);
    });

    // 页面加载事件
    // 监听页面所有资源加载完毕
    window.addEventListener("load", function () {
      // xxxxx
    });
    // 当初始的 HTML 文档被完全加载和解析完成之后就触发，而无需等待样式表、图像等完全加载
    document.addEventListener("DOMContentLoaded", function () {
      // xxxxx
    });

    // 元素滚动事件
    // 监听整个页面滚动
    window.addEventListener("scroll", function () {
      // xxxxx
    });

    // 页面尺寸事件
    // 会在窗口尺寸改变的时候触发事件
    window.addEventListener("resize", function () {
      // xxxxx
    });

    // 触摸事件
    // 手指触屏开始事件 touchstart
    span.addEventListener("touchstart", function () {
      console.log("我开始摸了");
    });
    // 手指触屏滑动事件 touchmove
    span.addEventListener("touchmove", function () {
      console.log("我一直摸");
    });

    // 手指触屏结束事件  touchend
    span.addEventListener("touchend", function () {
      console.log("我摸完了");
    });

    // 事件对象
    search.addEventListener("keyup", function (e) {
      if (e.key === "Enter") {
        alert("您按下了回车键");
      }
    });
  </script>
</body>
```

事件流

```html
<body>
  <div class="father">
    父盒子
    <div class="son">子盒子</div>
  </div>
  <script>
    const father = document.querySelector(".father");
    const son = document.querySelector(".son");

    // 事件捕获
    father.addEventListener(
      "click",
      function () {
        console.log("事件捕获 我是爸爸");
      },
      true
    );
    son.addEventListener(
      "click",
      function () {
        console.log("事件捕获 我是儿子");
      },
      true
    );

    // 事件冒泡
    father.addEventListener("click", function () {
      console.log("事件冒泡 我是爸爸");
    });
    son.addEventListener(
      "click",
      function (e) {
        console.log("事件冒泡 我是儿子");
        // e.stopPropagation();// 专门用来阻止事件冒泡
      },
      false
    );
  </script>
</body>
```

事件委托

```html
<body>
  <ul>
    <li>第1个孩子</li>
    <li>第2个孩子</li>
    <li>第3个孩子</li>
    <li>第4个孩子</li>
    <li>第5个孩子</li>
  </ul>
  <script>
    // 获取父元素ul
    const ul = document.querySelector("ul");
    // 给ul注册点击事件
    ul.addEventListener("click", function (e) {
      // console.dir(e.target.tagName) 得到目标元素的标签名
      if (e.target.tagName === "LI") {
        e.target.style.color = "pink";
      }
    });
  </script>
</body>
```

阻止默认行为

```html
<body>
  <form action="">
    姓名: <input type="text" name="username" />
    <button>提交</button>
  </form>
  <a href="http://www.baidu.com">点击跳转</a>
  <script>
    // 阻止默认行为 提交
    const form = document.querySelector("form");
    const input = document.querySelector("[name=username]");
    form.addEventListener("submit", function (e) {
      // 如果input表单的值为空则不允许提交
      if (input.value === "") {
        // return 无法阻止提交事件
        e.preventDefault(); // 阻止提交事件
      }
    });

    // 阻止默认行为 跳转
    document.querySelector("a").addEventListener("click", function (e) {
      e.preventDefault();
    });
  </script>
</body>
```

### DOM 节点

```html
<body>
  <ul>
    <li>我是第1个孩子</li>
    <li>我是第2个孩子</li>
    <li>我是第3个孩子</li>
    <li>我是第4个孩子</li>
  </ul>
  <script>
    const ul = document.querySelector("ul");
    const li2 = document.querySelector("ul li:nth-child(2)");

    // 查询父节点
    console.log(li2.parentNode);

    // 查询子节点
    console.log(ul.children);

    // 查询兄弟节点
    console.log(li2.previousElementSibling); // 上一个兄弟
    console.log(li2.nextElementSibling); // 下一个兄弟

    // 追加元素
    // 追加给父元素中 最后面
    const new_li1 = document.createElement("li");
    new_li1.innerHTML = "我是新加的1";
    ul.append(new_li1);
    // 追加给父元素中 最前面
    const new_li2 = document.createElement("li");
    new_li2.innerHTML = "我是新加的2";
    ul.prepend(new_li2);

    // 删除元素
    li2.remove();
  </script>
</body>
```

### 定时器

```html
<script>
  let setTimeoutId = setTimeout(function () {
    console.log("我只执行一次");
  }, 3000);
  let setIntervalId = setInterval(function () {
    console.log("我会不停的执行");
  }, 3000);

  clearTimeout(setTimeoutId);
  clearTimeout(setIntervalId);
</script>
```

### location

```html
<body>
  <form><input type="text" name="search" /> <button>搜索</button></form>
  <a href="#/music">音乐</a>
  <a href="#/download">下载</a>

  <button class="reload">刷新页面</button>
  <script>
    // location 对象
    // 1. href属性 （重点） 得到完整地址，赋值则是跳转到新地址
    console.log(location.href);
    // location.href = "http://www.baidu.com";

    // 2. search属性  得到 ? 后面的地址
    console.log(location.search); // ?search=笔记本

    // 3. hash属性  得到 # 后面的地址
    console.log(location.hash);

    // 4. reload 方法  刷新页面
    const btn = document.querySelector(".reload");
    btn.addEventListener("click", function () {
      // location.reload() // 页面刷新
      location.reload(true); // 强制页面刷新 ctrl+f5
    });
  </script>
</body>
```

### navigator

```html
<script>
  // 检测 userAgent（浏览器信息）
  (function () {
    const userAgent = navigator.userAgent;
    // 验证是否为Android或iPhone
    const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/);
    const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/);
    console.log(userAgent, android, iphone);
    // 如果是Android或iPhone，则跳转至移动站点
    // if (android || iphone) {
    //   location.href = "...";
    // }
  })();
</script>
```

### histroy

```html
<body>
  <button class="back">←后退</button>
  <button class="forward">前进→</button>
  <script>
    // 1.前进
    const forward = document.querySelector(".forward");
    forward.addEventListener("click", function () {
      // history.forward()
      history.go(1);
    });
    // 2.后退
    const back = document.querySelector(".back");
    back.addEventListener("click", function () {
      // history.back()
      history.go(-1);
    });
  </script>
</body>
```

### 本地存储

```html
<script>
  const goods = {
    name: "小米",
    price: 1999,
  };

  // 存储
  localStorage.setItem("goods", JSON.stringify(goods));

  // 获取
  console.log(JSON.parse(localStorage.getItem("goods")));

  // 删除
  localStorage.removeItem("goods");
</script>
```

## js

### 运算符

```html
<script>
  // 算术运算符：乘法 `\*` 、除法 `/` 、加法 `+` 、减法 `-`、取模（取余数）`%`
  // 赋值运算符：`=`、加法赋值`+=`、减法赋值`-+`、乘法赋值`*=`、除法赋值`/=`、取余赋值`%=`
  // 自增/自减运算符：自增`++`、自减`--`
  // 比较运算符：大于`>`、小于`<`、大于或等于`>=`、小于或等于`<=`、全等`===`、相等`==`、不相等`!=`、不全等`!==`
  // 逻辑运算符：逻辑与`&&`一假则假、逻辑或`||`一真则真、逻辑非`!`真变假，假变真、

  // 运算符优先级:
  // `()`
  // `++ -- !`
  // 先`* / %`后`+ -`
  // `> >= < <=`
  // `== != === !==`
  // 先`&&`后`||`
  // `=`
</script>
```

### 类型转换

显示转换

```html
<script>
  // 1 转换为数字类型
  // 1.1 把字符串转换为数字型 Number() 最常用的一种方式 推荐
  console.log(typeof Number("1")); // 1   number
  console.log(Number("abcd")); // NaN 如果无法完成转换则返回NaN
  // 1.2 把布尔值转换为数字型 true false
  console.log(Number(true)); // 1
  console.log(Number(false)); // 0
  // 1.3 把 null undefined 转换为数字型
  console.log(Number(null)); // 0
  console.log(Number(undefined)); // NaN
  // 1.4 parseInt() 和 parseFloat() 固定使用场景的   100px 只要100 不要px
  console.log(parseInt("100px")); // 100
  console.log(parseInt("100.5px")); // 100  parseInt() 只保留整数
  console.log(parseFloat("100.5px")); // 100.5 parseFloat() 可以返回小数

  // 2 转换为字符串类型
  // 2.1 String(数据) 开发中提倡使用这种方式
  console.log(String(1)); // '1'
  console.log(String(true)); // 'true'
  // 2.2 变量.toString(进制)
  let num = 10;
  console.log(num.toString()); //  string
  console.log(num.toString(10)); //  string   '10'
  console.log(num.toString(8)); //  string   '12'

  // 3. 转换为布尔型 Boolean
  // 以下为false，其余的都为true
  console.log(Boolean(false)); // false
  console.log(Boolean(0)); // false
  console.log(Boolean("")); // false
  console.log(Boolean(null)); // false
  console.log(Boolean(undefined)); // false
  console.log(Boolean(NaN)); // false
</script>
```

隐式转换

```html
<script>
  // 1. 隐式转换为数字型的运算符
  console.log(8 - "3"); // 5
  console.log("1999" * "2"); //  3998
  console.log(3 > "1"); // true
  console.log(3 == "3"); // true
  console.log(+"123"); // 123

  // 2. 隐式转换为字符串型的运算符
  console.log("pink" + 18); // "pink18"
  console.log("" + 18); // '18'

  // 3. 隐式转换为布尔型的运算符
  console.log(!true); // false
  console.log(!0); // true
  console.log(!""); // true
  console.log(!null); // true
  console.log(!undefined); // true
  console.log(!NaN); // true
  console.log(!false); // true
  console.log(!"pink"); // false
</script>
```

### 逻辑中断

```html
<script>
  // 1. 逻辑与中断：如果左边为假，则中断，如果左边为真，则返回右边的值
  console.log(false && 1 + 2); // false
  console.log(0 && 1 + 2); // 0
  console.log("" && 1 + 2); // ''
  console.log(undefined && 1 + 2); // undefined
  console.log(true && 1 + 2); // 3 此处不会发生逻辑中断
  console.log(1 && 1 + 2); // 3 此处不会发生逻辑中断

  // 2. 逻辑或中断，如果左侧为真，则中断，如果左侧为假，则返回右边的值
  console.log(true || 1 + 2); // true  发生了中断
  console.log(1 || 1 + 2); // 1  发生了中断
  console.log(false || 1 + 2); // 3 此处不会发生逻辑中断
</script>
```

### 闭包

一个函数对周围状态的引用捆绑在一起，闭包让开发者可以从内部函数访问外部函数的作用域

闭包 = 内层函数 + 外层函数的变量

闭包存在的问题：可能会造成内存泄漏

```html
<script>
  // 统计函数的调用次数
  function outer() {
    let count = 0;
    function fn() {
      count++;
      console.log(`函数被调用${count}次`);
    }
    return fn;
  }
  const re = outer();
  re();
  re();
</script>
```

### this

```html
<button class="btn1">点击</button>
<button class="btn2">5秒后启用</button>
<script>
  // 指向调用者
  console.log(this); // window
  function fn() {
    console.log(this); // window
  }
  fn();

  // 对象方法里面的this
  const obj = {
    name: "andy",
    sayHi: function () {
      console.log(this); // obj
    },
  };
  obj.sayHi();

  // 箭头函数的中this指向-沿用上一层作用域的this
  const fn = () => {
    console.log(this); // window
  };
  fn();

  const obj = {
    name: "andy",
    sayHi: () => {
      console.log(this); // window
    },
  };
  obj.sayHi();

  const obj = {
    name: "andy",
    sayHi: function () {
      const fun = () => {
        console.log(this); // obj
      };
      fun();
    },
  };
  obj.sayHi();

  // 构造函数内this
  function Person() {
    this.name = name;
    console.log(this);
  }
  const zs = new Person();

  // 特殊调用 call  apply  bind 可以改变this指向
  const o = { name: "佩奇" };
  function fun() {
    console.log(this);
  }
  fun.call(o);

  // 根据需求来选择是否使用箭头函数 this
  document.querySelector(".btn1").addEventListener("click", function () {
    this.style.color = "red";
  });

  document.querySelector(".btn2").addEventListener("click", function () {
    this.disabled = true;
    setTimeout(() => {
      console.log(this);
      this.disabled = false;
    }, 5000);
  });
</script>
```

### 构造函数、prototype 原型对象、proto 原型、constructor 属性、原型链、静态成员、实例成员

```html
<script>
  // 构造函数 this指向实例对象
  function Person(name, age) {
    // 实例成员 通过构造函数创建的对象称为实例对象，实例对象中的属性和方法称为实例成员(实例属性和实例方法)
    // 实例属性
    this.name = name;
    this.age = age;
    // 实例方法
    this.hello = function () {
      console.log("我是", this.name);
    };
  }

  // 原型对象上添加公共方法 可避免重复开辟内存空间 this指向构造函数
  Person.prototype = {
    // 指定constructor 指回构造函数
    constructor: Person,
    sing() {
      console.log(this.name, "我会唱歌");
    },
  };

  // 静态成员 构造函数的属性和方法被称为静态成员（静态属性和静态方法）this指向构造函数
  Person.hello = function () {
    console.log("我是", this.name);
  };

  // 实例化
  const zs = new Person("张三", 18);

  // 实例对象通过__proto__指向原型对象
  console.log(zs.__proto__);
  // 构造函数通过prototype指向原型对象
  console.log(Person.prototype);
  // 原型对象通过constructor指向构造函数;
  console.log(zs.__proto__.constructor);
  console.log(Person.prototype.constructor);

  //静态成员只能构造函数来访问,静态方法中的 this 指向构造函数
  Person.hello();

  // 原型链为对象成员查找机制提供一条路线
  console.log(zs.__proto__); // Person
  console.log(zs.__proto__.__proto__); // Object
  console.log(zs.__proto__.__proto__.__proto__); // null

  // instanceof 检测构造函数的原型对象是否在实例对象的原型链上
  console.log(zs instanceof Person);
  console.log(zs instanceof Object);
</script>
```

### 原型继承

```html
<script>
  // 父级Person构造函数
  function Person() {
    this.eyes = 2;
  }
  Person.prototype.eat = function () {
    console.log("我会吃饭");
  };

  // 继承-借助于原型对象 父级的实例对象覆盖自己的原型对象
  Man.prototype = new Person();
  Man.prototype.constructor = Man;
  // 子级Man构造函数
  function Man(name) {
    this.name = name;
  }

  // 继承-借助于原型对象 父级的实例对象覆盖自己的原型对象
  Woman.prototype = new Person();
  Woman.prototype.constructor = Woman;
  // 子级Woman构造函数
  function Woman(name) {
    this.name = name;
  }
  Woman.prototype.baby = function () {
    console.log("我会生孩子");
  };

  // 实例化
  const zs = new Man("张三");
  const ls = new Woman("李四");

  console.log(zs.name, zs, zs.__proto__);
  console.log(ls.name, ls, ls.__proto__);
</script>
```

### 拷贝

浅拷贝

```html
<script>
  // 只能对浅层基本数据类型有效，对于深层次的引用数据类型，修改任何一个对象，另一个对象都会变化

  const obj = {
    name: "佩奇",
  };
  const arr = ["佩奇", "跳泥坑", "唱歌"];

  // 1. 对象的浅拷贝
  // 1.1 Object.assign()
  const newObj = {};
  Object.assign(newObj, obj);
  newObj.name = "乔治";
  console.log(newObj, obj);

  // 1.2 ...展开运算符
  const newObj = { ...obj };
  newObj.name = "乔治";
  console.log(newObj, obj);

  // 2. 数组的浅拷贝
  // 2.1 .concat()
  const arr1 = [];
  const newArr = arr1.concat(arr);
  newArr[1] = "乔治";
  console.log(newArr, arr);

  // 2.2 ...展开运算符
  const newArr = [...arr];
  newArr[1] = "乔治";
  console.log(newArr, arr);
</script>
```

深拷贝

```html
<!-- 引入lodash库 -->
<script src=" https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js "></script>
<script>
  const obj = {
    name: "佩奇",
    love: undefined,
    family: {
      father: "猪爸爸",
    },
    hobby: ["跳泥坑", "唱歌"],
    sayHi() {
      console.log("我会唱歌");
    },
  };

  // 1. JSON序列化（常用的方式）会忽略 function undefined
  const newObj = JSON.parse(JSON.stringify(obj));
  newObj.family.father = "dad";
  console.log(newObj, obj);

  // 2. lodash 库实现
  const newObj = _.cloneDeep(obj);
  newObj.family.father = "dad";
  console.log(newObj, obj);

  // 3. 递归实现深拷贝 - 简版实现对象和数组的拷贝
  // 封装深拷贝函数 cloneDeep()
  function cloneDeep(oldObj) {
    // 先判断拷贝的是数组还是对象
    const newObj =
      Object.prototype.toString.call(oldObj) === "[object Array]" ? [] : {};
    // 遍历拷贝属性和值
    for (let k in oldObj) {
      // 把旧对象的值给新对象的属性
      if (typeof oldObj[k] === "object") {
        // 如果属性值是引用数据类型，则需要递归再次拷贝
        newObj[k] = cloneDeep(oldObj[k]);
      } else {
        // 否则属性值是基本数据类型，则直接赋值即可
        newObj[k] = oldObj[k];
      }
    }
    // 返回新对象
    return newObj;
  }
  const newObj = cloneDeep(obj);
  newObj.family.father = "dad";
  console.log(newObj, obj);
</script>
```

### try catch

```html
<script>
  function foo() {
    try {
      const p = document.querySelector("p");
      p.style.color = "red";
    } catch (error) {
      // 抛出异常
      throw new Error("异常", error.message);
    } finally {
      console.log("finally一定会执行");
    }
    console.log("如果出现错误，我的语句不会执行");
  }
  foo();
</script>
```

### call、apply、bind

使用 `call` 方法调用函数，同时指定函数中 `this` 的值

```html
<script>
  // 精确检测数据类型
  // Object.prototype.toString()  返回的结果是[object xxx类型]
  console.log(Object.prototype.toString.call("123")); // [object String]
  console.log(Object.prototype.toString.call(123)); // [object Number]
  console.log(Object.prototype.toString.call([])); // [object Array]
  console.log(Object.prototype.toString.call(null)); // [object Null]
</script>
```

使用 `apply` 方法调用函数（参数必须是数组），同时指定函数中 `this` 的值

```html
<script>
  // 求数组的最大值/最小值
  // 相当于...展开运算符
  console.log(Math.max.apply(null, [8, 2, 3])); // 8
  console.log(Math.min.apply(null, [8, 2, 3])); // 2
</script>
```

`bind` 方法并不会调用函数，而是创建一个指定了 `this` 值的新函数

```html
<button class="code">发送验证码</button>
<script>
  // 不需要调用函数，但是又想改变函数内部的this指向
  // 发送短信5秒倒计时业务
  const codeBtn = document.querySelector(".code");
  let flag = true;
  codeBtn.addEventListener("click", function () {
    if (flag) {
      // 关闭开关
      flag = false;
      let i = 5;
      this.innerHTML = `0${i}秒后重新获取`;
      // 定时器
      let timerId = setInterval(
        function () {
          i--;
          this.innerHTML = `0${i}秒后重新获取`;
          if (i === 0) {
            // 打开开关
            flag = true;
            this.innerHTML = `重新获取`;
            clearInterval(timerId);
          }
        }.bind(this),
        1000
      );
    }
  });
</script>
```

### 防抖

防抖: 单位时间内，频繁触发事件，只执行最后一次

- 搜索框搜索输入。只需用户最后一次输入完，再发送请求
- 手机号、邮箱验证输入检测

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>防抖</title>
    <style>
      .box {
        width: 500px;
        height: 500px;
        background-color: #ccc;
        color: #fff;
        text-align: center;
        font-size: 100px;
      }
    </style>
  </head>

  <div class="box"></div>
  <!-- 引入lodash库 -->
  <script src=" https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js "></script>
  <script>
    const box = document.querySelector(".box");
    let i = 1;
    function mouseMove() {
      box.innerHTML = i++;
    }

    // 1. _.debounce(fun, 时间)
    // box.addEventListener("mousemove", _.debounce(mouseMove, 500));

    // 2. 手写防抖函数 debounce(fu, 时间)
    function debounce(fn, t) {
      let timer = null;
      return function () {
        if (timer) clearTimeout(timer);
        timer = setTimeout(function () {
          fn();
        }, t);
      };
    }
    box.addEventListener("mousemove", debounce(mouseMove, 500));
  </script>
</html>
```

### 节流

节流：单位时间内，频繁触发事件，只执行一次

- 高频事件:鼠标移动 mousemove、页面尺寸缩放 resize、滚动条滚动 scroll 等等

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>节流</title>
    <style>
      .box {
        width: 500px;
        height: 500px;
        background-color: #ccc;
        color: #fff;
        text-align: center;
        font-size: 100px;
      }
    </style>
  </head>

  <div class="box"></div>
  <!-- 引入lodash库 -->
  <script src=" https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js "></script>
  <script>
    const box = document.querySelector(".box");
    let i = 1;
    function mouseMove() {
      box.innerHTML = i++;
    }
    // 1 .throttle(fun, 时间);
    box.addEventListener("mousemove", _.throttle(mouseMove, 3000));

    // 2. 节流的核心就是利用定时器(setTimeout) 来实现
    function throttle(fn, t) {
      let timer = null;
      return function () {
        if (timer) return;
        timer = setTimeout(function () {
          fn();
          timer = null;
        }, t);
      };
    }
    box.addEventListener("mousemove", throttle(mouseMove, 3000));
  </script>
</html>
```

