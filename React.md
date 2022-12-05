# React
## 簡介
![](https://i.imgur.com/aX5KJnc.png)
:::info
將數據渲染為HTML視圖的開源JavaScript庫
:::
> 為甚麼使用
1. 原生JS操作DOM繁瑣，效率低(DOM-API操作UI) 
2. 使用JS直接操作DOM，瀏覽器會進行大量的重繪重排
3. 原生JS沒有組件化編碼方案，代碼復用率低

> React 特點
1. 採用**組件化模式、聲明式編碼**，提高開發效率及組件復用率
2. 在React Native中可以使用React語法進行移動端開發
3. 使用虛擬DOM+優秀的Diffing算法，盡量減少與真實DOM的交互

## 基本使用
### 相關JS庫
- react.js：react核心庫
- react-dom.js：提供操作dom的react擴展庫
- babel.min.js：解析jsx（JavaScript XML）代碼語法轉為js代碼的庫
### 創建虛擬dom的兩種方式
- 純js方式(一般不用)
- jsx方式
### 渲染虛擬dom
*語法*：ReactDOM.render(virtualDOM, containerDOM)
*作用*：將虛擬DOM元素渲染到頁面中的真實容器DOM顯示
*virtualDOM*：純JS或JSX創建的虛擬DOM對象
*containerDOM*：用來包含虛擬DOM元素的真實DOM元素(一般是一個div)
```javascript=
<body>
    <!-- 容器 -->
    <div id="test"></div>

    <!-- 引入核心庫 -->
    <script type="text/javascript" src="../js//react.development.js"></script>
    <!-- 引入dom 用於react操作dom -->
    <script
      type="text/javascript"
      src="../js/react-dom.development.js"
    ></script>
    <!-- 引入babel 轉jsx為js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>

    <script type="text/babel">
      // 創建虛擬dom
      const VDOM = (
        <h1 id="title">
          <span>hello react</span>
        </h1>
      );
      //渲染虛擬dom到頁面
      ReactDOM.render(VDOM, document.getElementById("test"));
    </script>
  </body>
```
### 關於虛擬dom
1. 本質是**object**類型的對象(一般對象)
2. 虛擬dom比較輕，真實dom比較重，虛擬dom為react內部使用，無需那麼多屬性
3. 虛擬dom最終會被react轉化為真實dom，呈現在頁面上
![](https://i.imgur.com/i7O7lkg.png)


##  React JSX
### 語法規則
1. 定義虛擬DOM時，**不需寫引號**
2. 標籤中混入JS表達式時要用 **{}**
3. 樣式的類名指定不要用clss，需用**className**
4. 內聯樣式要用style={{key:value}}的形式
5. 只能有**一個根標籤**
6. 標籤必須閉合
7. 標籤首字母
    - 小寫字母開頭，則將轉為html中同名元素，若html中無該標籤同名元素，則報錯
    - 大寫字母開頭，react將去渲染對應的組件，若組件沒有定義，則報錯

#### 區分【js語句(代碼)】與【js表達式】
創建虛擬dom中語法需用表達式
- 表達式：一個表達式會產生一個值，可以放在任何一個需要值的地方
    (1) a
    (2) a+b
    (3) arr.map()
    (4) function test(){}
- 語句：控制代碼走向
    (1) if(){}
    (2) for(){}
    (3) switch(){case:xxx}

```javascript=
<script type="text/babel">
      const data = ["Angular", "React", "Vue"];
      // 創建虛擬dom
      const VDOM = (
        <div>
          <h1>前端js框架</h1>
          <ul>
            {data.map((item, index) => {
              return <li key={index}>{item}</li>;
            })}
          </ul>
        </div>
      );
      //渲染虛擬dom到頁面
      ReactDOM.render(VDOM, document.getElementById("test"));
    </script>
```

## 模塊與組件
### 模塊
- 理解：向外提供特定功能的js程序, 一般就是一個js文件
- why：業務邏輯增加，代碼越來越多且複雜
- 作用：複用js，簡化js的編寫，提高js運行效率
- 模塊化：當應用的js都以模塊來編寫，這個應用就是模塊化的應用
### 組件
- 理解：用來實現局部功能效果的代碼和資源的集合(html/css/js/image等等)
- why：一個介面的功能更複雜
- 作用：複用編碼，簡化項目編碼，提高運行效率
- 組件化：當應用是以多組件的方式實現，這就是一個組件化的應用

# 面向組件編程
## 函數式組件
```javascript=
 <script type="text/babel">
        //創建函數式組件
        function MyComponet(){
            console.log(this);//undefined，babel編譯後開啟嚴格模式(禁止自訂義函數指向window)
            return <h2>函數定義的組件，簡單組件</h2>
        }
      ReactDOM.render(<MyComponet/>, document.getElementById("test"));
    </script>
```
執行了ReactDOM.render(<MyComponet/>...)之後過程：
1. React解析組件標籤，找到了MyComponent組件
2. 發現組件式使用函數定義，隨後調用該函數，將返回的虛擬DOM轉為真實DOM，呈現在頁面中

---

## 類式組件
```javascript=
 <script type="text/babel">
      //創建類式組件
      class MyComponet extends React.Component {
        render() {
            //render是放在MyComponet的原型對象上，供實例使用
            //render中的this是MyComponet的實例對象 <=> MyComponet組件實例對象
          return <h2>類定義的組件，複雜組件</h2>;
        }
      }
      ReactDOM.render(<MyComponet />, document.getElementById("test"));
    </script>
```
執行了ReactDOM.render(<MyComponet/>...)之後過程：
1. React解析組件標籤，找到了MyComponent組件
2. 發現組件式使用類式定義，隨後new出該類的實例，並通過該實例調用到原型上的render方法
3. 將render返回的虛擬DOM轉為真實DOM，呈現在頁面中
## 組件三大核心-state
> 案例-定義一個顯示天氣訊息的組件，默認炎熱或涼爽，點擊切換
> 
step1
```javascript=
 <script type="text/babel">
      //創建組件
      class Weather extends React.Component {
        constructor(props) {
          super(props);
          //初始化狀態
          this.state = { isHot: true };
        }
        render() {
          //讀取狀態
          const isHot = this.state;
          //demo函數不能加()直接調函數，只需指定函數給onClick作為回調
          return <h1 onClick={changeWeather}>今天天氣{isHot ? "炎熱" : "涼爽"}</h1>;
        }
      }
      //渲染組件到頁面
      ReactDOM.render(<Weather />, document.getElementById("test"));

      function changeWeather(){
        console.log('被點擊了');
      } 
    </script>
```
step2(加上功能)
```javascript=
   <script type="text/babel">
      //創建組件
      class Weather extends React.Component {
        constructor(props) {
          super(props);
          //初始化狀態
          this.state = { isHot: true };
          //解決changeWeather中this指向問題
          this.changeWeather = this.changeWeather.bind(this);
        }
        render() {
          //讀取狀態
          const { isHot } = this.state;
          return (
            <h1 onClick={this.changeWeather}>
              今天天氣{isHot ? "炎熱" : "涼爽"}
            </h1>
          );
        }
        changeWeather() {
         //獲取原來isHot值
          const isHot = this.state.isHot;
          //狀態必須通過setState更新，且更新是一種合併，不是替換
          this.setState({ isHot: !isHot });
        }
      }
      //渲染組件到頁面
      ReactDOM.render(<Weather />, document.getElementById("test"));
    </script>
```
簡化寫法(構造器、自定義方法)
```javascript=
    <script type="text/babel">
      //創建組件
      class Weather extends React.Component {
        //初始化狀態
        state = { isHot: true };

        render() {
          const { isHot } = this.state;
          return (
            <h1 onClick={this.changeWeather}>
              今天天氣{isHot ? "炎熱" : "涼爽"}
            </h1>
          );
        }

        //自定義方法---要用賦值語句的形式+箭頭函數
        changeWeather = () => {
          const isHot = this.state.isHot;
          this.setState({ isHot: !isHot });
        };
      }
      
      //渲染組件到頁面
      ReactDOM.render(<Weather />, document.getElementById("test"));
    </script>
```
### state說明
> 理解
- state是組件對象最重要的屬性，值是對象(可以包含多個key-value的組合)
- 組件被稱為'狀態機'，透過更新組件的state來更新對應的頁面顯示
>注意
- 組件中render方法中的this為組件實例對象
- 組件自訂義的方法中this為undefined，如何解決?
    - 強制綁定this:通過函數對象的bind()
    - 賦值語句+箭頭函數
- 狀態數據，不能直接修改或更新
## 組件三大核心-props
> 案例-自定義一個顯示人員信息的組件
    - 姓名必須指定填寫，且為字符串類型
    - 性別為字符串類型，默認為男
    - 年齡為數字類型，實際年齡+1，默認18


```javascript=
    <script type="text/babel">
      class Person extends React.Component {
        //對標籤屬性進行類型、必要性限制，需引入prop-type.js文件
        static propTypes = {
          name: PropTypes.string.isRequired,
          sex: PropTypes.string,
          age: PropTypes.number,
          speak: PropTypes.func, //func限制speak為函數
        };

        //默認標籤屬性值
        static defaultProps = {
          sex: "男",
          age: 18,
        };

        render() {
          const { name, age, sex } = this.props;
          return (
            <ul>
              <li>姓名:{name}</li>
              <li>性別:{sex}</li>
              <li>年齡:{age + 1}</li>
            </ul>
          );
        }
      }

      ReactDOM.render(
        <Person name="tom" age={19} sex="male" speak={speak} />,
        document.getElementById("test1")
      );

      const p = { name: "ben", age: 18, sex: "male" };
      ReactDOM.render(<Person {...p} />, document.getElementById("test2"));

      function speak() {
        console.log(hi);
      }
    </script>
```
---
函數式組件寫法
```javascript=
    <script type="text/babel">
      function Person(props) {
        const { name, age, sex } = props;
        return (
          <ul>
            <li>姓名:{name}</li>
            <li>性別:{sex}</li>
            <li>年齡:{age + 1}</li>
          </ul>
        );
      }
      //需引入prop-type.js文件
      Person.propTypes = {
        name: PropTypes.string.isRequired,
        sex: PropTypes.string,
        age: PropTypes.number,
        speak: PropTypes.func, //限制speak為函數
      };

      //默認標籤屬性值
      Person.defaultProps = {
        sex: "不男不女",
        age: 18,
      };

      ReactDOM.render(
        <Person name="tom" age={19} sex="male" speak={speak} />,
        document.getElementById("test1")
      );

      const p = { name: "ben", age: 18, sex: "male" };
      ReactDOM.render(<Person {...p} />, document.getElementById("test2"));

      function speak() {
        console.log(hi);
      }
    </script>
```

### props說明
> 理解
- 每個組件對象都會有props(properties)屬性
- 組件標籤的所有屬性都保存在props中
>作用
- 通過標籤屬性從組件外向組件內傳遞變化的數據
- 組件內部的不能修改props數據

## 组件三大核心-refs
> 案例
    > 1. 點擊按鈕，顯示第一個輸入框中的值
    > 2. 當第二個輸入框失去焦點時，顯示這個輸入框中的值 
### string類型refs(不建議使用-效率問題)
```javascript=
 <script type="text/babel">
      class Demo extends React.Component {
        showData = () => {
          // const { input1 } = this.refs;
          alert(this.refs.input1.value);
        };
        showData2 = () => {
          const { input2 } = this.refs;
          alert(input2.value);
        };
        render() {
          return (
            <div>
              <input ref="input1" type="text" placeholder="點擊按鈕提示數據" />
              &nbsp;
              <button onClick={this.showData}>點我提示左側數據</button>&nbsp;
              <input
                ref="input2"
                onBlur={this.showData2}
                type="text"
                placeholder="失去焦點提示數據"
              />
            </div>
          );
        }
      }
      ReactDOM.render(<Demo/>, document.getElementById("test1"));
    </script>
```
### 回調函數形式refs
```javascript=
    <script type="text/babel">
      class Demo extends React.Component {
        showData = () => {
          // const { input1 } = this.refs;

          alert(this.input1.value);
        };
        showData2 = () => {
          const { input2 } = this;
          alert(input2.value);
        };
        render() {
          return (
            <div>
              <input
                //把ref當前所處的節點掛在實例自身上，並且取名input1
                //react內聯回調函數會有傳送兩次的情況
                ref={(c) => (this.input1 = c)} //currentNode = c
                type="text"
                placeholder="點擊按鈕提示數據"
              />
              &nbsp;
              <button onClick={this.showData}>點我提示左側數據</button>&nbsp;
              <input
                ref={(c) => (this.input2 = c)}
                onBlur={this.showData2}
                type="text"
                placeholder="失去焦點提示數據"
              />
            </div>
          );
        }
      }
      ReactDOM.render(<Demo/>, document.getElementById("test1"));
    </script>
```
### creatRefs
```javascript=
    <script type="text/babel">
      class Demo extends React.Component {
        // React.createRef2調用後可以返回一個容器，該容器可以存儲被ref所標示的節點，該容器是專人專用
        myRef = React.createRef();
        myRef2 = React.createRef();
        showData = () => {
          alert(this.myRef.current.value);
        };
        showData2 = () => {
          const { input2 } = this;
          alert(this.myRef2.current.value);
        };
        render() {
          return (
            <div>
              <input
                ref={this.myRef}
                type="text"
                placeholder="點擊按鈕提示數據"
              />
              &nbsp;
              <button onClick={this.showData}>點我提示左側數據</button>&nbsp;
              <input
                ref={this.myRef2}
                onBlur={this.showData2}
                type="text"
                placeholder="失去焦點提示數據"
              />
            </div>
          );
        }
      }
      ReactDOM.render(<Demo/>, document.getElementById("test1"));
    </script>
```

### Refs理解
>理解
- 組件內的標籤可以定義ref屬性來標示自己
    
>編碼
- **字符串形式的ref**
        <input ref="input1"/>
- **回調形式的ref**
        <input ref = { c => {this.input1 = c }}
- **createRef**
    myRef = React.createRef()
    <input ref = {this.myRef}/>
    
### 事件處理
- 通過onXxx屬性指定事件處理函數(注意大小寫)
    - React使用的是自定義(合成)事件，而不是使用原生的DOM事件
    - React中的事件是通過事件委託方式處理(委託給組件最外層元素)
- 通過event.target得到發生事件的DOM元素對象
```javascript=
    <script type="text/babel">
      class Demo extends React.Component {
        // React.createRef2調用後可以返回一個容器，該容器可以存儲被ref所標示的節點，該容器是專人專用
        myRef = React.createRef();
        myRef2 = React.createRef();
        showData = (event) => {
          alert(this.myRef.current.value);
        };
        showData2 = (event) => {
          alert(event.target.value);
        };
        render() {
          return (
            <div>
              <input
                ref={this.myRef}
                type="text"
                placeholder="點擊按鈕提示數據"
              />
              &nbsp;
              <button onClick={this.showData}>點我提示左側數據</button>&nbsp;
              <input
                //發生事件的元素是要操控的元素可省略ref
                onBlur={this.showData2}
                type="text"
                placeholder="失去焦點提示數據"
              />
            </div>
          );
        }
      }
      ReactDOM.render(<Demo />, document.getElementById("test1"));
    </script>
```
## 非受控組件
#### 不受react組件狀態控制，手動操作dom的方式
```javascript=
 <script type="text/babel">
      class Login extends React.Component {
        handleSubmit = (event) => {
          event.preventDefault();//阻止表單提交
          const { username, password } = this;
          alert(`用戶名:${username.value},密碼:${password.value}`);
        };
        render() {
          return (
            <form onSubmit={this.handleSubmit}>
              用戶名:
              <input
                ref={(c) => (this.username = c)}
                type="text"
                name="username"
              />
              密碼:
              <input
                ref={(c) => (this.password = c)}
                type="password"
                name="password"
              />
              <button>登錄</button>
            </form>
          );
        }
      }
      ReactDOM.render(<Login />, document.getElementById("test1"));
    </script>
```
## 受控組件
#### 被react組件狀態控制
```javascript=
<script type="text/babel">
      class Login extends React.Component {
        //初始化狀態
        state = {
          username: "",
          password: "",
        };

        //保存用戶名到狀態中  
        saveUsername = (event) => {
          this.setState({ username: event.target.value });
        };

        //保存密碼到狀態中
        savePassword = (event) => {
          this.setState({ password: event.target.value });
        };

        //表單提交的回調
        handleSubmit = (event) => {
          event.preventDefault(); //阻止表單提交
          const { username, password } = this.state;
          alert(`用戶名:${username},密碼:${password}`);
        };
        render() {
          return (
            <form onSubmit={this.handleSubmit}>
              用戶名:
              <input 
                onChange={this.saveUsername} 
                type="text" 
                name="username" />
              密碼:
              <input
                onChange={this.savePassword}
                type="password"
                name="password"
              />
              <button>登錄</button>
            </form>
          );
        }
      }
      ReactDOM.render(<Login />, document.getElementById("test1"));
    </script>
```

### 高階函數 - 柯里化
高階函數:
1. 若函數接收的參數是一個函數，則可稱為高階函數
2. 若函數調用的返回值依然是一個函數，則也可稱為高階函數

函數的柯里化:
- 通過函數調用繼續返回函數的方式，實現多次接收參數，最後統一處理的函數編碼形式。

```javascript=
    <script type="text/babel">
      class Login extends React.Component {
        //初始化狀態
        state = {
          username: "",
          password: "",
        };

        //保存表單數據到狀態中  (柯里化)
        saveFormData = (dataType) => {
            return (event) => {
                this.setState({
                    [dataType]:event.target.value
                })
            }
        };

        //表單提交的回調
        handleSubmit = (event) => {
          event.preventDefault(); //阻止表單提交
          const { username, password } = this.state;
          alert(`用戶名:${username},密碼:${password}`);
        };
        render() {
          return (
            <form onSubmit={this.handleSubmit}>
              用戶名:
              <input 
                onChange={this.saveFormData('username')} 
                type="text" 
                name="username" />
              密碼:
              <input
                onChange={this.saveFormData('password')}
                type="password"
                name="password"
              />
              <button>登錄</button>
            </form>
          );
        }
      }
      ReactDOM.render(<Login />, document.getElementById("test1"));
    </script>
```
### 不用柯里化寫法
```javascript=
    <script type="text/babel">
      class Login extends React.Component {
        //初始化狀態
        state = {
          username: "",
          password: "",
        };

        //保存表單數據到狀態中  
        saveFormData = (dataType,event) => {
          this.setState({[dataType]:event.target.value})
        };

        //表單提交的回調
        handleSubmit = (event) => {
          event.preventDefault(); //阻止表單提交
          const { username, password } = this.state;
          alert(`用戶名:${username},密碼:${password}`);
        };
        render() {
          return (
            <form onSubmit={this.handleSubmit}>
              用戶名:
              <input 
                onChange={(event) => {this.saveFormData('username',event)}} 
                type="text" 
                name="username" />
              密碼:
              <input
                onChange={(event) => {this.saveFormData('password',event)}}
                type="password"
                name="password"
              />
              <button>登錄</button>
            </form>
          );
        }
      }
      ReactDOM.render(<Login />, document.getElementById("test1"));
    </script>
```
## 組件的生命周期
```javascript=
    <script type="text/babel">
      //創建組件
      class Life extends React.Component {
        state = { opacity: 1 };
        death = () => {
          //卸載組件
          ReactDOM.unmountComponentAtNode(document.getElementById("test1"));
        };

        //組件掛載完畢
        componentDidMount() {
          this.timer = setInterval(() => {
            //獲取原狀態
            let { opacity } = this.state;
            //減小0.1
            opacity -= 0.1;
            if (opacity <= 0) opacity = 1;
            // 設置新透明度
            this.setState({ opacity }); //this.setState({ opacity = opacity });
          }, 200);
        }

        //組件將要卸載
        componentWillUnmount() {
          //清除定時器
          clearInterval(this.timer);
        }

        // render調用時機:初始化渲染，狀態更新之後
        render() {
          return (
            <div>
              <h2 style={{ opacity: this.state.opacity }}>react學不會怎麼辦</h2>
              <button onClick={this.death}>不活了</button>
            </div>
          );
        }
      }
      ReactDOM.render(<Life />, document.getElementById("test1"));
    </script>
```
#### 理解
1. 組件從創建到死亡會經歷一些特定的階段
2. React組件中包含一系列**鉤子函數(生命週期回調函數)**，會在**特定時刻調用**
3. 定義組件時，會在特定的生命週期回調函數中，做特定的工作

### 生命週期三個階段
![](https://i.imgur.com/TSKQb2q.png)

1. **初始化階段**：由ReactDOM.render()觸發-初次渲染
    - constructor()
    - getDerivedStateFromProps
    - render()
    - componentDidMount()
3. **更新階段**：由組件內部this.setState()或父組件重新render觸發
    - getDerivedStateFromProps
    - shouldComponentUpdate()
    - render()
    - getSnapshotBeforeUpdate
    - componentDidUpdate()
5. **卸載組件**：由ReactDOM.unmountComponemtAtNode觸發
    - componentWillUnmount()

#### 重要的鉤子
- render:初始化渲染或更新渲染調用
- componentDidMount:開啟監聽，發送ajax請求
- componentWillUnmount:做一些收尾工作，如:清理定時器

## key原理
![](https://i.imgur.com/pERgdb9.png)
![](https://i.imgur.com/H0R2Pcx.png)

# React應用(基於腳手架)
## react腳手架
- 技術架構 react + webpack + es6 + eslint
- 快速創建一個模板項目
- 使用腳手架開發的項目具有:模塊化、組件化、工程化

### 項目結構
![](https://i.imgur.com/7sifabh.png)
![](https://i.imgur.com/wV7Y8XP.png)
### 組件化編碼流程
1. 拆分組件：拆分介面 抽取組件
2. 實現靜態組件：使用組件實現靜態頁面效果
3. 實現動態組件
    - 動態顯示初始化數據
        - 數據類型
        - 數據名稱
        - 保存在哪個組件
    - 交互(從綁定事件監聽開始)
### todolist_案例
### github搜尋_案例
## React 路由

