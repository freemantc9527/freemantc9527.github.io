# 多态详解

多态（Polymorphism）这个概念最早来自于生物学，表示的是同一物种在同一种群中存在两种或多种明显不同的表型。

而在面向对象编程思想中，这个概念表达的是具有共性的类型，在执行相同的行为时，会体现出不同的实现方式。我们可以简称为：相同的行为，不同的实现。（只有方法才有“多态”性的体现）

## 多态的分类

### 静态多态
静态多态是在编译期间就可以确定要执行的是何种类型的对象以及该对象的何种行为，运行期不会有改变的情况。

#### 重载
> 在一个类当中，具有多个同名方法，参数列表不同（包括：参数个数、参数类型、参数顺序的不同），从而各有各的实现。

*重载在我们日常开发中太过常见，所以不再举例子*

#### 重写
> 在继承关系中，不同的子类都拥有继承于父类的某个共有方法，但是各有各的实现。

```java
public abstract class Game {
    public abstract void play();
    public String info() {
        return "我是 Game";
    }
}

public class StarCraft extends Game {
    public void play() {
        // 玩 StarCraft 好爽
    }

    @Override
    public String info() {
        return "我是 StarCraft";
    }
}

public class LOL extends Game {
    public void play() {
        // 玩 LOL 好爽
    }

    @Override
    public String info() {
        return "我是 LOL";
    }
}

public class Player {
    private StarCraft game; //绑定对象
    public void go(){
        game.play();
    }
}
```

### 动态多态
> 当我们绑定一个父类引用的时候，它既有可能指向父类的对象，也有可能是指向该父类的某个子类的对象。它是可变的，具体指向谁不是由编码期的声明决定的，而是可以通过在运行时传入不同的对象，从而形成所谓的“动态绑定”。


#### 动态绑定
```java
public class Player {
    private Game game; //绑定父对象
    public void setGame(Game game) {
        this.game = game;
    }

    public void go(){
        game.play();
    }    
}

public class TestMain{
    public static void main(String[] args){
        Player player = new Player();
        player.setGame(new StarCraft()); //可以用配置文件来决定用哪个具体的类
        player.go();
    }
}
```

#### 可以扩展到哪些知识点
- 接口的引用也可以指向实现类的对象；
- 反射实现动态产生对象；
- Spring完成IoC注入；
- 桥梁模式、装饰器模式、策略模式等常见设计模式；
- 聚合组合原则、依赖倒转原则等常见设计原则。