# javascript高級
## 面向過程編程 POP(Process Oriented Programming)
![](https://i.imgur.com/DhbGS3X.png)




## 面向對象編程 OOP(Object Oriented Programming)
![](https://i.imgur.com/5WaRJiG.png)
![](https://i.imgur.com/8YqTfj5.png)
面相對象的特性:
- 封裝性
- 繼承性
- 多態性

![](https://i.imgur.com/rFCXMMv.png) 

## ES6中的類和對象
### 面向對像
![](https://i.imgur.com/wcH82hj.png)
### 對像
![](https://i.imgur.com/odjXEWK.png)
### 類 class
![](https://i.imgur.com/ui81mo5.png)
![](https://i.imgur.com/mVwJPiL.png)
### 創建類
![](https://i.imgur.com/yVVAzwu.png)

```javascript=
 <script>
      //創建一個person類
      class Person {
        //構造器方法
        constructor(name, age) {
          this.name = name; //構造器中的this > 類的實例對象
          this.age = age;
        }
        //一般方法
        speak() {
            //透過person實例調用speak時，speak中的this就是person實例
          console.log(`我叫${this.name},我的年齡是${this.age}`);
        }
      }
      //創建一個Person的實例對象
      const p1 = new Person("tom", 18);
      const p2 = new Person("jim", 20);

      console.log(p1);
      console.log(p2);
      p1.speak();
      p2.speak();
    </script>
```
**繼承**
```javascript=
 <script>
      //創建一個person類
      class Person {
        //構造器方法
        constructor(name, age) {
          this.name = name; //構造器中的this > 類的實例對象
          this.age = age;
        }
        //一般方法
        speak() {
          //透過person實例調用speak時，speak中的this就是person實例
          console.log(`我叫${this.name},我的年齡是${this.age}`);
        }
      }

      //創建一個Student類，繼承Person類
      class Student extends Person {
        constructor(name, age, grade) {
          super(name, age);
          this.grade = grade;
        }
        //重寫從父類繼承過來的方法
        speak() {
          console.log(
            `我叫${this.name},我的年齡是${this.age},我讀的是${this.grade}`
          );
        }
      }
      const s1 = new Student('小高', 15, '高一');
      console.log(s1);
      s1.speak();
    </script>
```

### 總結
1. 類中的構造器不是必須寫，要對實例進行一些初始化操作，如添加指定屬性時才寫
2. 如果A類繼承了B類，且A類中寫了構造器，那麼A類構造器中的super必須要調用
3. 類中所定義的方法，都是放在類的原型對象上，供實例去使用