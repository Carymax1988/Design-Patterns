# Design-Patterns
<p>转载网址<a href='http://blog.csdn.net/zhangerqing/article/details/8194653'>http://blog.csdn.net/zhangerqing/article/details/8194653</a></p><br />

设计模式<br />
<br />
设计模式的分类<br />
总体来说设计模式分为三大类：<br />
创建型模式，共五种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。<br />
结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。<br />
行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354152786_2930.jpg' /><br />
<br />
设计模式的六大原则<br />
1、开闭原则（Open Close Principle）<br />
<p>开闭原则就是说对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。所以一句话概括就是：为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类，后面的具体设计中我们会提到这点。</p><br />
2、里氏代换原则（Liskov Substitution Principle）<br />
<p>里氏代换原则(Liskov Substitution Principle LSP)面向对象设计的基本原则之一。 里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。 LSP是继承复用的基石，只有当衍生类可以替换掉基类，软件单位的功能不受到影响时，基类才能真正被复用，而衍生类也能够在基类的基础上增加新的行为。里氏代换原则是对“开-闭”原则的补充。实现“开-闭”原则的关键步骤就是抽象化。而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。—— From Baidu 百科</p><br />
3、依赖倒转原则（Dependence Inversion Principle）<br />
<p>这个是开闭原则的基础，具体内容：真对接口编程，依赖于抽象而不依赖于具体。</p><br />
4、接口隔离原则（Interface Segregation Principle）<br />
<p>这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。还是一个降低类之间的耦合度的意思，从这儿我们看出，其实设计模式就是一个软件的设计思想，从大型软件架构出发，为了升级和维护方便。所以上文中多次出现：降低依赖，降低耦合。</p><br />
5、迪米特法则（最少知道原则）（Demeter Principle）<br />
<p>为什么叫最少知道原则，就是说：一个实体应当尽量少的与其他实体之间发生相互作用，使得系统功能模块相对独立。</p><br />
6、合成复用原则（Composite Reuse Principle）<br />
<p>原则是尽量使用合成/聚合的方式，而不是使用继承。</p><br />

Java的23中设计模式<br />
1、工厂方法模式（Factory Method）<br />
普通工厂模式<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354156868_1191.PNG'/><br />
多个工厂方法模式<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354158145_2392.PNG' /><br />
静态工厂方法模式<br />
将上面的多个工厂方法模式里的方法置为静态的，不需要创建实例，直接调用即可。<br />
<p>总体来说，工厂模式适合：凡是出现了大量的产品需要创建，并且具有共同的接口时，可以通过工厂方法模式进行创建。在以上的三种模式中，第一种如果传入的字符串有误，不能正确创建对象，第三种相对于第二种，不需要实例化工厂类，所以，大多数情况下，我们会选用第三种——静态工厂方法模式。</p><br />
2、抽象工厂模式（Abstract Factory）<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354159363_7245.PNG' /><br />
<p>其实这个模式的好处就是，如果你现在想增加一个功能：发及时信息，则只需做一个实现类，实现Sender接口，同时做一个工厂类，实现Provider接口，就OK了，无需去改动现成的代码。这样做，拓展性较好！</p><br />
3、单例模式（Singleton）<br />
<p>实际情况是，单例模式使用内部类来维护单例的实现，JVM内部的机制能够保证当一个类被加载的时候，这个类的加载过程是线程互斥的。</p><br />
<p>public class Singleton {  
  
    /* 私有构造方法，防止被实例化 */  
    private Singleton() {  
    }  
  
    /* 此处使用一个内部类来维护单例 */  
    private static class SingletonFactory {  
        private static Singleton instance = new Singleton();  
    }  
  
    /* 获取实例 */  
    public static Singleton getInstance() {  
        return SingletonFactory.instance;  
    }  
  
    /* 如果该对象被用于序列化，可以保证对象在序列化前后保持一致 */  
    public Object readResolve() {  
        return getInstance();  
    }  
}</p>
