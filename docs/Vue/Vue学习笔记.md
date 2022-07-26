# Vue 核心

## 一、模板语法

在 html 中插入一些 js 语法代码

1. 插值语法（双大括号表达式）
2. 指令（以 v-开头）

### （一）插值语法

功能：用于解析标签体内容

语法：{{xxx}} ，xxxx 会作为 js 表达式解析

### （二）指令语法

功能：解析标签属性、解析标签体内容、绑定事件

举例：v-bind:href = 'xxxx' ，xxxx 会作为 js 表达式被解析

说明：Vue 中有有很多的指令，此处只是用 v-bind 举个例子

## 二、数据绑定

### （一）单向数据绑定

语法：v-bind:href ="xxx" 或简写为 :href

特点：数据只能从 data 流向页面

### （二）双向数据绑定

语法：v-mode:value="xxx" 或简写为 v-model="xxx"

特点：数据不仅能从 data 流向页面，还能从页面流向 data

> **额外知识**
>
> el 的两种写法
>
> 第一种：
>
> ```vue
> new Vue({ el:"#root", data:{ msg:"尚硅谷" } })
> ```
>
> 第二种：
>
> ```
> const vm = new Vue({
> 	data(){
> 		return name:'尚硅谷'
> 	}
> })
>
> vm.$mount('#root')
> ```
>
> data 的两种写法
>
> 第一种：
>
> ```
> new Vue({
> 	el:"#root",
> 	data:{
> 		msg:"尚硅谷"
> 	}
> })
> ```
>
> 第二种：
>
> ```
> const vm = new Vue({
> 	el:'#root',
> 	data(){
> 		return name:'尚硅谷' //绝对不能使用箭头函数
> 	}
> })
> ```

### （三）MVVM 模型

M：模型(Model) ：对应 data 中的数据

V：视图(View) ：模板

VM：视图模型(ViewModel) ： Vue 实例对象

## 三、事件处理

事件不要直接写到 data 对象中，会增加 vue 的负担，写入 methods 中，并且不要使用箭头符号，会导致 this 指向 window。

### （一）绑定监听

#### 1.v-on:xxx="fun"

```html
<body>
  <div id="root">
    <h2>欢迎来到{{name}}学习</h2>
    <button v-on:click="showInfo">点我提示信息</button>
  </div>

  <script>
    Vue.config.productionTip = false;

    new Vue({
      el: "#root",
      data: {
        name: "尚硅谷",
      },
      methods: {
        showInfo() {
          alert("同学你好");
        },
      },
    });
  </script>
</body>
```

#### 2.@xxx = "fun"

```html
<button @click="showInfo">点我提示信息</button>
```

#### 3.@xxx = "fun(参数)"

可以给 event 保留位置：@xxx = "fun($event, 参数)"

### （二）事件修饰符

> **注意：**修饰符可以连用，`@keyup.stop.prevent`

#### 1.prevent（常用）

阻止事件的默认行为 event.preventDefault()

#### 2.stop（常用）

阻止事件冒泡

#### 3.once（常用）

事件只触发一次

#### 4.capture

使用事件的捕获模式

#### 5.self

只有 event.target 是当前操作的元素时才触发事件

#### 6.passive

事件的默认行为为立即执行，无需等待事件回调执行完毕

```html
<body>
  <div id="root">
    <p>欢迎来到{{name}}学习</p>
    <!-- 1.阻止默认事件（常用） -->
    <a href="http://www.atguigu.com" @click.prevent="showInfo">点我弹出消息</a>
    <!-- 2.阻止事件冒泡 -->
    <div class="demo1" @click="showInfo">
      <button @click.stop="showInfo">点我提示信息</button>
    </div>
    <!-- 3.事件只触发一次 -->
    <button @click.once="showInfo">点我提示信息</button>
    <!-- 4.使用事件的捕获模式 -->
    <div class="box1" @click.capture="showMsg(1)">
      div1
      <div class="box2" @click="showMsg(2)">div2</div>
    </div>
    <!-- 5.self -->
    <div class="demo1" @click.self="showInfo">
      <button @click="showInfo">点我提示信息</button>
    </div>
    <!-- 6.passive -->
    <ul @wheel.passive="demo" class="list">
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
    </ul>
  </div>

  <script>
    Vue.config.productionTip = false;

    const vm = new Vue({
      el: "#root",
      data: {
        name: "尚硅谷",
      },
      methods: {
        showInfo(e) {
          alert("同学你好!");
          console.log(e.target);
        },
        showMsg(msg) {
          console.log(msg);
        },
        demo() {
          console.log("@");
        },
      },
    });
  </script>
</body>
```

### （三）键盘修饰符

#### 1.keycode

操作的是某个 keycode 值的键

```html
<input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo" />
```

**Vue 中常用的案件别名：**

| 键                            | 别名  | 键                         | 别名   |
| ----------------------------- | ----- | -------------------------- | ------ |
| 回车                          | enter | 删除（捕获“删除”和“退格”） | delete |
| 退出                          | esc   | 空格                       | space  |
| 换行（闭合配合 keydown 使用） | tab   | 上                         | up     |
| 下                            | down  | 左                         | left   |
| 右                            | right |                            |        |

> Vue 未提供别名的按键，可以使用按键原始的 key 值去绑定，多个单词组成的 key 值要转为 kebab-case（短横线命名）

特殊修饰键：`ctrl` `alt` `shift` `meta`

（1）配合 keyup 使用：按下修饰键的同事，再按下其它键，随后释放其它键，事件才被触发。

（2）配合 keydown 使用：正常触发事件。

> **注意：**keyCode 已经废弃，不推荐使用指定具体的按键。

不推荐定制按键别名：`Vue.config.keyCodes.自定义键名 = 键码`

#### 2..keyName

操作的某个按键名的键(少部分)

### （四）计算属性与监视

1.计算属性-computed

要显示的数据不存在，要通过计算得来。

在页面中使用`{{方法名}}`来显示计算的结果

```html
<body>
  <div id="root">
    姓：<input type="text" v-model="firstName" /><br /><br />
    名：<input type="text" v-model="lastName" /><br /><br />
    姓名：<span>{{fullName}}</span>
  </div>

  <script>
    Vue.config.productionTip = false;

    new Vue({
      el: "#root",
      data: {
        firstName: "张",
        lastName: "三",
      },
      computed: {
        fullName: {
          get() {
            return this.firstName + "-" + lastName;
          },
          set(value) {
            console.log("set" + value);
            const arr = value.split("-");
            this.firstName = arr[0];
            this.lastName = arr[1];
          },
        },
      },
    });
  </script>
</body>
```
