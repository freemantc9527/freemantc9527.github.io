# 工厂模式

## 优点
- 可以使代码结构清晰，有效地封装变化。在编程中，产品类的实例化有时候是比较复杂和多变的，通过工厂模式，将产品的实例化封装起来，使得调用者根本无需关心产品的实例化过程，只需依赖工厂即可得到自己想要的产品。
- 对调用者屏蔽具体的产品类。如果使用工厂模式，调用者只关心产品的接口就可以了，至于具体的实现，调用者根本无需关心。即使变更了具体的实现，对调用者来说没有任何影响。
- 降低耦合度。产品类的实例化通常来说是很复杂的，它需要依赖很多的类，而这些类对于调用者来说根本无需知道，如果使用了工厂方法，我们需要做的仅仅是实例化好产品类，然后交给调用者使用。对调用者来说，产品所依赖的类都是透明的。

## 适用场景
- 作为一种创建型模式，在任何需要生成复杂对象的地方，都可以使用工厂方法模式。
- 工厂模式是一种典型的解耦模式，迪米特法则在工厂模式中表现的尤为明显。
- 由于工厂模式是依靠抽象架构的，它把实例化产品的任务交由实现类完成，扩展性比较好。

## 示例代码

示例：简单工厂
```csharp
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            // 快餐店点一份汉堡
            Food food1 = Restaurant.Create("汉堡");
            food1.Cook();

            // 快餐店点一份薯条
            Food food2 = Restaurant.Create("薯条");
            food2.Cook();
        }
    }

    public abstract class Food
    {
        // 输出做了什么食物
        public abstract void Cook();
    }

    public class Hamburger : Food
    {

        public override void Cook()
        {
            Console.WriteLine("做了一份汉堡！");
        }
    }

    public class FrenchFries : Food
    {
        public override void Cook()
        {
            Console.WriteLine("做了一份薯条！");
        }
    }

    public class Restaurant
    {
        public static Food Create(string name)
        {
            Food food = null;
            if (name.Equals("汉堡"))
            {
                food = new Hamburger();
            }
            else if (name.Equals("薯条"))
            {
                food = new FrenchFries();
            }

            return food;
        }
    }
}
```

示例：工厂方法
```csharp
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            // 初始化汉堡店和薯条店
            Factory.Restaurant rt1 = new Factory.HamburgerRestaurant();
            Factory.Restaurant rt2 = new Factory.FrenchFriesRestaurant();

            // 汉堡店点一份汉堡
            Factory.Food fhb1 = rt1.CreateFoodFactory();
            fhb1.Cook();

            // 薯条店点一份薯条
            Factory.Food fhb2 = rt2.CreateFoodFactory();
            fhb2.Cook();
        }
    }

    public abstract class Food
    {
        // 输出做了什么食物
        public abstract void Cook();
    }

    public class Hamburger : Food
    {

        public override void Cook()
        {
            Console.WriteLine("汉堡店做了一份汉堡！");
        }
    }

    public class FrenchFries : Food
    {
        public override void Cook()
        {
            Console.WriteLine("薯条店做了一份薯条！");
        }
    }

    /// <summary>
    /// 抽象工厂类
    /// </summary>
    public abstract class Restaurant
    {
        // 工厂方法
        public abstract Food CreateFoodFactory();
    }

    public class HamburgerRestaurant : Restaurant
    {

        public override Food CreateFoodFactory()
        {
            return new Hamburger();
        }
    }

    public class FrenchFriesRestaurant : Restaurant
    {
        public override Food CreateFoodFactory()
        {
            return new FrenchFries();
        }
    }
```

示例：抽象工厂
```csharp
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            // 要一份肯德基的汉堡
            BrandFood rt1 = new Kfc();
            AbstractFactory.Hamburger hb1 = rt1.CreateHamburger();
            hb1.Cook();

            // // 要一份麦当劳的汉堡
            BrandFood rt2 = new Mcdonalds();
            AbstractFactory.Hamburger hb2 = rt2.CreateHamburger();
            hb2.Cook();
        }
    }

    /// <summary>
    /// 品牌食物
    /// </summary>
    public abstract class BrandFood
    {
        public abstract Hamburger CreateHamburger();
    }

    public class Kfc : BrandFood
    {
        public override Hamburger CreateHamburger()
        {
            return new KfcHamburger();
        }
    }

    public class Mcdonalds : BrandFood
    {

        public override Hamburger CreateHamburger()
        {
            return new McdonaldsHamburger();
        }
    }

    /// <summary>
    /// 汉堡抽象类
    /// </summary>
    public abstract class Hamburger
    {
        public abstract void Cook();
    }

    public class KfcHamburger : Hamburger
    {
        public override void Cook()
        {
            Console.WriteLine("肯德基——香辣鸡腿堡");
        }
    }

    public class McdonaldsHamburger : Hamburger
    {
        public override void Cook()
        {
            Console.WriteLine("麦当劳——麦辣鸡腿堡");
        }
    }
}
```
