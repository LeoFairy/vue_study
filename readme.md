# vue_study

> 一套用于构建用户界面的渐进式Javascript框架



## 1.初步认识

![image-20241112115641892](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241112115641892.png)



## 2. 插值语法

插值语法 放在标签体内

指令语法 管理标签属性 

![image-20241112170956409](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241112170956409.png)





## 3. 数据绑定

v-model双向绑定： 就是把输入的内容 去影响到vue实例 

![image-20241112171244405](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241112171244405.png)

![image-20241112171400711](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241112171400711.png)



```
    <div id="root">
      <!--普通方式
          单项数据绑定： <input type="text" v-bind:value="name"> <br>
     双项数据绑定： <input type="text" v-model:value="name"> -->

      <!-- 简写方式： -->
      单项数据绑定： <input type="text" :value="name" /> <br />
      双项数据绑定： <input type="text" v-model="name" />
    </div>
```



## 4. el与data的两种写法



### 4.1  el的两种写法

- 写法一： 

  直接指定 。  如上略

- 写法二： **使用$mount指定**

  ```
   const v = new Vue({
    //  el:'#root',
     data: {
      name:'vue'
     }
     })
     console.log(v);
    //  v.$mount('#root')  // 使用$mount 来指定vue实例对应的容器
      
    setTimeout(() => {
       v.$mount('#root') 
    }, 1000);
  ```

### 4.2 data的两种写法

- 写法一：对象式

  如上略

- 写法二：**函数式**   （必须要返回一个对象）

```
   //data的第二种写法： 函数式  不能写成箭头函数 
  new Vue({
   el:'#root',
   //还可以去掉冒号  去掉function
   data:function(){
    return{
       name: 'vue'
    }
   }
   })
```

==学到组件时 要用函数式来写==

由Vue管理的函数，一定不要写箭头函数， 否则this就不再指Vue实例， 而是windows



## 5.MVVM模型

![image-20241112181006641](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241112181006641.png)

![image-20241112181417564](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241112181417564.png)



## 6.数据代理

###  6.1 object.defineproperty

 这个方法增加的属性，默认没有办法被枚举、被修改、被删除  需要设置配置对象。

如果要枚举， 那么要在配置对象中增加 enumerable

```
 let person ={
      name:'张三',
      sex:'男'
    }

    // 三个属性：  对象、 属性 、 配置对象
    Object.defineProperty(person,'age',{
      value:18,
      enumerable:true, //控制属性是否可以枚举  ，默认不可以
      writable:true ,//控制属性是否可以被修改 ， 默认不可以
      configurable:true, //控制属性是否可以被删除， 默认不可以
      
      //当有人读取person的age属性时，get函数 (getter)就会被调用，且返回值就是age值
      get(){
        return number
      },

      //当游人修改person的age属性时，set函数（setter）就会被调用，且会收到修改的具体的值
      set(value){
        console.log('有人修改了age属性，且值为',value);
        number=value
      }

    })
```



### 6.2数据代理



通过vm对象 去修改 data里面的 name的值

要访问 data里面的值，  要用 ==vm._data==  ， 



![image-20241113093615556](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113093615556.png)



## 7.事件处理

### 7.1 事件的基本使用

![image-20241113094940287](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113094940287.png)

```
<div id="root">
      <h2>欢迎来到{{name}}学习</h2>
      <button @click="showInfo1">点我提示信息1(不传参)</button>
      <button @click="showInfo2(66,$event)">点我提示信息(传参)</button>
</div>
   w <script>
      new Vue({
        el: "#root",
        data: {
          name: "vue",
        },
        methods: {
          showInfo1(event) {
            // console.log(event.target.innerText);

            // console.log(this); // this指的是vm

            alert("同学你好");
          },
          showInfo2(number, event) {
            console.log(number);

            // console.log(event.target.innerText);

            // console.log(this); // this指的是vm

            alert("同学你好呀");
          },
        },
      });
    </script>
```



### 7.2 事件修饰符

![image-20241113100325875](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113100325875.png)

![image-20241113102347636](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113102347636.png)

**事件修饰符可以多个使用**

![image-20241113102436771](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113102436771.png)



### 7.3 键盘事件

![image-20241113102317556](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113102317556.png)



.ctrl.y  加上y  ， 那么只有按下ctry+y再松开y 会触发。   如果 不写.y ，那么ctrl加上其他按键都会触发

![image-20241113102611239](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113102611239.png)



## 8.计算属性

### 8.1 基本内容

![image-20241113110934276](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113110934276.png)



```
 new Vue({
        el: "#root",
        data: {
          firstName: "张",
          latsName: "三",
        },
        computed: {
          fullName: {
            //当有人读取fullName时，get就会调用,且返回值就作为fullName的值
            // get什么时候调用？: 1.初次读取fullName时 。2. 所依赖的数据发生变化时
            get() {
              console.log("get被调用");
              return this.firstName + "-" + this.latsName;
            },
            //当fullName被修改时，set就会被调用
            set(value) {
              console.log("set", value);
              // 张-三   李-四
              const arr = value.split("-");
              this.firstName = arr[0];
              this.latsName = arr[1];
            },
          },
        },
      });
```



### 8.2 简写

==计算属性简写： (仅限于 只读不写)==

```
    computed: {
          //简写：
          fullName() {
            console.log("get被调用");
            return this.firstName + "-" + this.latsName;
          },
        },
```





## 9.监视属性

### 9.1 基本内容

![image-20241113113659323](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113113659323.png)



- 写法一： 在vue内：

  ```
    watch: {
            isHot: {
              // immediate  初始化时 让handler调度一下
              immediate: true,
              // 当isHot的值发生改变时就会调用handler
              handler(newValue, oldValue) {
                console.log("isHot被修改了", newValue, oldValue);
              },
            },
          },
  ```

  

- 写法二：

  ```
     vm.$watch("isHot", {
          // immediate  初始化时 让handler调度一下
          immediate: true,
          // 当isHot的值发生改变时就会调用handler
          handler(newValue, oldValue) {
            console.log("isHot被修改了", newValue, oldValue);
          },
        });
  ```



### 9.2 深度监视

![image-20241113114920266](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113114920266.png)



监视多级结构中某个属性的变化：

```
  watch: {
          isHot: {
            // 当isHot的值发生改变时就会调用handler
            handler(newValue, oldValue) {
              console.log("isHot被修改了", newValue, oldValue);
            },
          },
          //监视多级结构中某个属性的变化
          "numbers.a": {
            handler() {
              console.log("a被改变了");
            },
          },
        },
```

监视多级结构中所有属性的变化

```
numbers: {
            deep: true,
            handler() {
              console.log("numbers被改变了");
            },
          },
```



### 9.3 监视属性简写



-  写法一简写：

  ```  
    //简写： 方法内只有handler
            isHot(newValue, oldValue) {
              console.log("isHot被修改了", newValue, oldValue);
            },
  ```

- 写法二简写：

  ``` 
  vm.$watch("isHot", function () {
          console.log("isHot被修改了", newValue, oldValue);
        });
  ```

  

==计算属性vs监视属性==

- 计算属性不可以开启异步任务去维护数据。

![image-20241113153015092](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113153015092.png)



## 10.绑定样式 



### 10.1  绑定class样式

代码：

```
  <div id="root">
      <!-- 绑定class样式 --字符串写法，适用于：样式的类名不确定，需要动态指定 -->
      <div class="basic normal" :class="mood" @click="changeMood">{{name}}</div>
      <br /><br />
      <!-- 绑定class样式 --数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
      <div class="basic" :class="classArr">{{name}}</div>

      <!-- 绑定class样式 --对象写法，适用于：要绑定的样式个数确定、名字也确定 ,   但要动态决定用不用  -->
      <div class="basic" :class="classObj">{{name}}</div>
    </div>
    <script>
      new Vue({
        el: "#root",
        data: {
          name: "vue",
          mood: "normal",
          classArr: ["style1", "style2", "style3"],
          classObj: {
            style1: true,
            style2: false,
          },
        },
        methods: {
          changeMood() {
            const arr = ["happy", "sad", "normal"];
            const index = Math.floor(Math.random() * 3); //生成0 1 2 随机
            this.mood = arr[index];
          },
        },
      });
```

### 10.2 绑定style

![image-20241113160912657](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113160912657.png)

```
 <!-- ① style样式绑定： 对象写法 -->
      <!--   错误的：  <div class="basic" :style="font-size:fontsize;">{{name}}</div> -->
      <!-- style 动态  要写成对象， 名：值。  属性名不对 要把杠去掉， 杠后面要大写， -->
      <!--  即： <div class="basic" :style="{fontSize: fontsize +'px'}">{{name}}</div> -->
      <div class="basic" :style="styleObj">{{name}}</div>

      <!-- ② style样式绑定： 数组写法 -->
      <div class="basic" :style="[styleObj,styleObj2]">{{name}}</div>
```

 样式对象，红色框内的为样式对象。  样式对象中 绿色的属性名部分 不能乱写， 必须是存在的。

<img src="C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113161009438.png" alt="image-20241113161009438" style="zoom:50%;" />



## 11.条件渲染

![image-20241113162704737](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113162704737.png)

代码：

```
 <div id="root">
      <!-- 使用v-show做条件渲染  变化频率高-->
      <!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->
      <!-- <h2 v-show="1===1">欢迎来到{{name}}</h2> -->

      <!-- 使用v-if做条件渲染 -->
      <!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->
      <!-- <h2 v-if="1 ===1">欢迎来到{{name}}</h2> -->

      <h2>当前的n值是{{n}}</h2>
      <button @click="n++">点我n+1</button>

      <div v-if="n===1">Angular</div>
      <div v-if="n===2">React</div>
      <div v-if="n===3">Vue</div>

      <!-- 第一个成立后面不会再看了 多个if建议还是用elseif -->
      <!-- 四个要一起用，中间不能加东西。中断后的不能用了 -->
      <div v-if="n===1">Angular</div>
      <div v-else-if="n===2">React</div>
      <div v-else-if="n===3">Vue</div>
      <div v-else>Vue</div>

      <!-- v-if与template -->
      <!-- template不会破坏原有的结构。 只能跟着v-if用 -->
      <template v-if="n===1">
        <h2>你好</h2>
        <h2>vue</h2>
        <h2>北京</h2>
      </template>
    </div>
```



## 12.列表渲染

### 12.1基本列表

![image-20241113165155513](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113165155513.png)

遍历代码：

```
 <!--遍历数组 -->
      <h2>人员列表</h2>
      <ul>
        <li v-for="(p,index) of people" :key="index">{{p.name}}-{{p.age}}</li>
      </ul>

      <!-- 遍历对象 -->
      <h2>汽车信息</h2>
      <ul>
        <li v-for="(value,k) of car" :key="k">{{k}}----{{value}}</li>
      </ul>

      <!-- 遍历字符串-->
      <h2>遍历字符串</h2>
      <ul>
        <li v-for="(char,index) of str" :key="index">{{char}}----{{index}}</li>
      </ul>

      <!-- 遍历指定次数-->
      <h2>遍历指定次数</h2>
      <ul>
        <li v-for="(number,index) of 5" :key="index">
          {{index}}----{{number}}
        </li>
      </ul>
```



### 12.2 Key的原理

-  index作为key

进行了破坏原有顺序的 ，会出现问题

![image-20241113170130309](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113170130309.png)



- id作为key

![image-20241113170340268](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113170340268.png)





没写key 时， 默认为index







==vue中的key有什么作用？  key的内部原理==

![image-20241113170655297](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113170655297.png)

![image-20241113170725020](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113170725020.png)



### 12.3列表过滤

> 正常是直接用计算属性，  但初学为了好理解， 先学习watch来实现列表过滤



- watch实现：

  ```
   new Vue({
          el: "#root",
          data: {
            keyWord: "",
            people: [
              {
                id: "001",
                name: "马冬梅",
                age: 18,
                sex: "女",
              },
              {
                id: "002",
                name: "周冬雨",
                age: 19,
                sex: "女",
              },
              {
                id: "003",
                name: "周杰伦",
                age: 20,
                sex: "男",
              },
              {
                id: "003",
                name: "温兆伦",
                age: 21,
                sex: "男",
              },
            ],
            filPeople: [],
          },
          watch: {
            keyWord: {
              immediate: true,
              handler(val) {
                // filter 不更改原来的， 只会生成新的
                // console.log('keyWord被修改',val);
                this.filPeople = this.people.filter((p) => {
                  return p.name.indexOf(val) !== -1; //包含 把位置告诉，  不包含结果为-1
                });
              },
            },
          },
        });
  ```

  



-  computed 实现

  ```
   computed: {
            filPeople() {
              return this.people.filter((p) => {
                return p.name.indexOf(this.keyWord) !== -1;
              });
            },
          },
  ```

  

###  12.4 列表排序



```
 computed: {
          filPeople() {
            const arr = this.people.filter((p) => {
              return p.name.indexOf(this.keyWord) !== -1;
            });
            //判断一下是否需要排序   sortType 为1和2时 都为true， 只有0是false
            if (this.sortType) {
              arr.sort((p1, p2) => {
                return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age;
              });
            }
            return arr;
          },
        },
```

### 12.5 Vue监测数据改变的原理

>Vue监视数据的原理：
>
>				1. vue会监视data中所有层次的数据。
>	
>				2. 如何监测对象中的数据？
>						通过setter实现监视，且要在new Vue时就传入要监测的数据。
>						(1).对象中后追加的属性，Vue默认不做响应式处理
>						(2).如需给后添加的属性做响应式，请使用如下API：
>										Vue.set(target，propertyName/index，value) 或
>									    vm.$set(target，propertyName/index，value)
>	
>				3. 如何监测数组中的数据？
>									通过包裹数组更新元素的方法实现，本质就是做了两件事：
>										(1).调用原生对应的方法对数组进行更新。
>										(2).重新解析模板，进而更新页面。
>	
>				4.在Vue修改数组中的某个元素一定要用如下方法：
>							1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
>							2.Vue.set() 或 vm.$set()
>	
>				特别注意：Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！！！
>			    注: 数据劫持可以理解成为vue对你写在data的数据会进行加工，让它们都变成响应式的



对象的监测

![image-20241113181053109](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241113181053109.png)





-  Vue.set（）  在已经创建好的vm上 增加属性：

  >  只能给data里面的对象增加属性，   不能直接给vm上就加属性**

  ![image-20241114095100114](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114095100114.png)

![image-20241114095125714](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114095125714.png)

由于数据代理 vm._data.student = vm.student  ， 所以可以简写为：

![image-20241114095253432](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114095253432.png)

![image-20241114095300483](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114095300483.png)

代码

```
   methods: {
          addSex() {
            // Vue.set(this.student, "sex", "男");
            this.$set(this.student, "sex", "男");
          },
        },
```



监测数组， 得是在数组调用自身的7种修改了数组的方法，不包括filter 因为filter不修改原本数组。 如果要筛选 ，可以在筛选完之后再修改那个原数组。

<img src="C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114101541594.png" alt="image-20241114101541594" style="zoom:50%;" />

vue对数组的变更方法进行了包裹， 在原来Array.prototype的变更方法基础上，增加了重新解析模版的功能， 所以也能达到监测数据的功能。

<img src="C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114101824376.png" alt="image-20241114101824376" style="zoom: 50%;" />

同样也可以采用set方法来 对数组监测。

![image-20241114102104555](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114102104555.png)

## 13.收集表单数据

>收集表单数据：
>					若：<input type="text"/>，则v-model收集的是value值，用户输入的就是value值。
>					若：<input type="radio"/>，则v-model收集的是value值，且要给标签配置value值。
>					若：<input type="checkbox"/>
>							1.没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值）
>							2.配置input的value属性:
>									(1)v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
>									(2)v-model的初始值是数组，那么收集的的就是value组成的数组
>					备注：v-model的三个修饰符：
>									lazy：失去焦点再收集数据
>									number：输入字符串转为有效的数字
>									trim：输入首尾空格过滤





## 14. 过滤器

>过滤器：
>				定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
>				语法：
>						1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}
>						2.使用过滤器：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"
>				备注：
>						1.过滤器也可以接收额外参数、多个过滤器也可以串联
>						2.并没有改变原本的数据, 是产生新的对应的数据



-  局部过滤器:

  ```
    filters: {
            timeFormater(value, str = "YYYY年MM月DD日 HH:mm:ss") {
              return dayjs(value).format(str);
            },
          },
  ```

  

- 全局过滤器

  ```
   //全局过滤器：
        Vue.filter("mySlice", function (value) {
          return value.slice(0, 4);
        });
  ```

  

- 过滤器实现：

  ```
    <!-- 过滤器实现 -->
        <h3>现在是：{{time | timeFormater}}</h3>
        <!-- 过滤器传参 -->
        <h3>现在是：{{time | timeFormater('YYYY_MM_DD')}}</h3>
        <!-- 过滤器串联 -->
        <h3>现在是：{{time | timeFormater('YYYY_MM_DD')| mySlice}}</h3>
     
  ```

  



## 15. 内置指令

### 15.1. 学过的指令：

>我们学过的指令：
>					v-bind	: 单向绑定解析表达式, 可简写为 :xxx
>					v-model	: 双向数据绑定
>					v-for  	: 遍历数组/对象/字符串
>					v-on   	: 绑定事件监听, 可简写为@
>					v-if 	 	: 条件渲染（动态控制节点是否存存在）
>					v-else 	: 条件渲染（动态控制节点是否存存在）
>					v-show 	: 条件渲染 (动态控制节点是否展示)
>



### 15.2.v-text

>v-text指令：
>					1.作用：向其所在的节点中渲染文本内容。 (纯文本渲染)
>					2.与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。这里有点不太灵活



### 15.3 v-html

>
>
>v-html指令：
>						1.作用：向指定节点中渲染包含html结构的内容。
>						2.与插值语法的区别：
>									(1).v-html会替换掉节点中所有的内容，{{xx}}则不会。
>									(2).v-html可以识别html结构。
>						3.严重注意：v-html有安全性问题！！！！
>									(1).在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。
>									(2).一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！





cookie 原理

![image-20241114145616417](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114145616417.png)



### 15.4 v-cloak指令

>   v-cloak指令（没有值）：
>                 1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
>                 2.使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。



#### 15.5v-once指令

> v-once指令：
> 						1.v-once所在节点在初次动态渲染后，就视为静态内容了。
> 						2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。



### 15.6v-pre指令

> v-pre指令：
> 					1.跳过其所在节点的编译过程。
> 					2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。

用于不用解析的语句处



## 16. 自定义指令



```
自定义指令总结：
			一、定义语法：
						(1).局部指令：
							new Vue({directives:{指令名:配置对象} })  
                            或  new Vue({directives: {指令名:回调函数}})
						(2).全局指令：
							Vue.directive(指令名,配置对象) 或  Vue.directive(指令名,回调函数)

			二、配置对象中常用的3个回调：
						(1).bind：指令与元素成功绑定时调用。
						(2).inserted：指令所在元素被插入页面时调用。
						(3).update：指令所在模板结构被重新解析时调用。

			三、备注：
				         1.指令定义时不加v-，但使用时要加v-；
						 2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。
						 						（user-name）				（userName）
```





## 17. 生命周期

> 生命周期：
> 				1.又名：生命周期回调函数、生命周期函数、生命周期钩子。
> 				2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。
> 				3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。
> 			    4.生命周期函数中的this指向是vm 或 组件实例对象。

### 17.1 mounted

vue完成模版的解析并把==初始的==真实的DOM元素放入页面后（挂载完毕）调用mounted

  

### 17.2 分析生命周期：

在beforeUpdate中页面和数据还没同步



在beforeDestory 上修改数据，  是不会触发更新页面的，

![image-20241114163222078](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241114163222078.png)

![image-20241115093518523](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241115093518523.png)



### 17.3 总结生命周期

``` 
常用的生命周期钩子：
				1.mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。
				2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。

			关于销毁Vue实例
				1.销毁后借助Vue开发者工具看不到任何信息。
				2.销毁后自定义事件会失效，但原生DOM事件依然有效。(click之类的原生事件依然会被调用)
			    3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。
```



## 18. 非单文件组件

组件：实现应用中**局部**功能**代码**和**资源**的**集合** 

一个文件中包含n个组件

### 18.1 基本使用



```
Vue中使用组件的三大步骤：
                    一、定义组件(创建组件)
                    二、注册组件
                    三、使用组件(写组件标签)

            一、如何定义一个组件？
                        使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；
                        区别如下：
                                1.el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
                                2.data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。
                        备注：使用template可以配置组件结构。

            二、如何注册组件？
                            1.局部注册：靠new Vue的时候传入components选项
                            2.全局注册：靠Vue.component('组件名',组件)

            三、编写组件标签：
                            <school></school>
```



### 18.2  注意事项



```
几个注意点：
					1.关于组件名:
								一个单词组成：
											第一种写法(首字母小写)：school
											第二种写法(首字母大写)：School
								多个单词组成：
											第一种写法(kebab-case命名)：my-school
											第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持)
								备注：
										(1).组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。
										(2).可以使用name配置项指定组件在开发者工具中呈现的名字。

					2.关于组件标签:
								第一种写法：<school></school>
								第二种写法：<school/>
								备注：不用使用脚手架时，<school/>会导致后续组件不能渲染。

					3.一个简写方式：
								const school = Vue.extend(options) 可简写为：const school = options
```





### 18.3VueComponent

```

			关于VueComponent：
						1.school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的。

						2.我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，
							即Vue帮我们执行的：new VueComponent(options)。

						3.特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent！！！！注意这一点很重要

						4.关于this指向：
								(1).组件配置中：
											data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【VueComponent实例对象】。
								(2).new Vue(options)配置中：
											data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。

						5.VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。
							Vue的实例对象，以后简称vm。 vm管理着一个又一个vc，vc可以再
					    6.因为组件是可复用的 Vue 实例，所以它们与 new Vue 接收相同的选项，例如 data、computed、watch、methods 以及生命周期钩子等。仅有的例外是像 el 这样根实例特有的选项。
					      所以vm与vc属性配置并不是一模一样，尽管vc底层复用了很多vm的逻辑
```





## 18.4 重要的内置关系

> ​         1.一个重要的内置关系：==VueComponent.prototype.__proto__ =====Vue.prototype====
> ​			2.为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。



![image-20241118105624091](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241118105624091.png)







## 19. 单文件组件

一个文件中包含1个组件

 书写标准： ![image-20241118110446897](C:/Users/11426/AppData/Roaming/Typora/typora-user-images/image-20241118110446897.png)


