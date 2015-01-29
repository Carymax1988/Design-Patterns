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

<ol start="1" class="dp-j"><li class="alt"><span><span class="keyword">public</span><span>&nbsp;</span><span class="keyword">class</span><span>&nbsp;Singleton&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;私有构造方法，防止被实例化&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;Singleton()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;此处使用一个内部类来维护单例&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;</span><span class="keyword">class</span><span>&nbsp;SingletonFactory&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;Singleton&nbsp;instance&nbsp;=&nbsp;</span><span class="keyword">new</span><span>&nbsp;Singleton();&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;获取实例&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;Singleton&nbsp;getInstance()&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;SingletonFactory.instance;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;如果该对象被用于序列化，可以保证对象在序列化前后保持一致&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;Object&nbsp;readResolve()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;getInstance();&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>}&nbsp;&nbsp;</span></li></ol>
<br />
<p>也有人这样实现：因为我们只需要在创建类的时候进行同步，所以只要将创建和getInstance()分开，单独为创建加synchronized关键字，也是可以的：</p><br />
<ol start="1" class="dp-j"><li class="alt"><span><span class="keyword">public</span><span>&nbsp;</span><span class="keyword">class</span><span>&nbsp;SingletonTest&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;SingletonTest&nbsp;instance&nbsp;=&nbsp;</span><span class="keyword">null</span><span>;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;SingletonTest()&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;</span><span class="keyword">synchronized</span><span>&nbsp;</span><span class="keyword">void</span><span>&nbsp;syncInit()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">if</span><span>&nbsp;(instance&nbsp;==&nbsp;</span><span class="keyword">null</span><span>)&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;instance&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;SingletonTest();&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;SingletonTest&nbsp;getInstance()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">if</span><span>&nbsp;(instance&nbsp;==&nbsp;</span><span class="keyword">null</span><span>)&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;syncInit();&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;instance;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>}&nbsp;&nbsp;</span></li></ol>
<br />
<p>补充：采用"影子实例"的办法为单例对象的属性同步更新</p><br />
<ol start="1" class="dp-j"><li class="alt"><span><span class="keyword">public</span><span>&nbsp;</span><span class="keyword">class</span><span>&nbsp;SingletonTest&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;SingletonTest&nbsp;instance&nbsp;=&nbsp;</span><span class="keyword">null</span><span>;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;Vector&nbsp;properties&nbsp;=&nbsp;</span><span class="keyword">null</span><span>;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;Vector&nbsp;getProperties()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;properties;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;SingletonTest()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;</span><span class="keyword">synchronized</span><span>&nbsp;</span><span class="keyword">void</span><span>&nbsp;syncInit()&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">if</span><span>&nbsp;(instance&nbsp;==&nbsp;</span><span class="keyword">null</span><span>)&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;instance&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;SingletonTest();&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;SingletonTest&nbsp;getInstance()&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">if</span><span>&nbsp;(instance&nbsp;==&nbsp;</span><span class="keyword">null</span><span>)&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;syncInit();&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;instance;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">void</span><span>&nbsp;updateProperties()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SingletonTest&nbsp;shadow&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;SingletonTest();&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;properties&nbsp;=&nbsp;shadow.getProperties();&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>}&nbsp;&nbsp;</span></li></ol>
<br />
4、建造者模式（Builder）<br />
<p>工厂类模式提供的是创建单个类的模式，而建造者模式则是将各种产品集中起来进行管理，用来创建复合对象，所谓复合对象就是指某个类具有不同的属性</p><br />
5、原型模式（Prototype）<br />
浅复制：将一个对象复制后，基本数据类型的变量都会重新创建，而引用类型，指向的还是原对象所指向的。<br />
深复制：将一个对象复制后，不论是基本数据类型还有引用类型，都是重新创建的。<br />
<ol start="1" class="dp-j"><li class="alt"><span><span class="keyword">public</span><span>&nbsp;</span><span class="keyword">class</span><span>&nbsp;Prototype&nbsp;</span><span class="keyword">implements</span><span>&nbsp;Cloneable,&nbsp;Serializable&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;</span><span class="keyword">final</span><span>&nbsp;</span><span class="keyword">long</span><span>&nbsp;serialVersionUID&nbsp;=&nbsp;1L;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;String&nbsp;string;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;SerializableObject&nbsp;obj;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;浅复制&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;Object&nbsp;clone()&nbsp;</span><span class="keyword">throws</span><span>&nbsp;CloneNotSupportedException&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Prototype&nbsp;proto&nbsp;=&nbsp;(Prototype)&nbsp;<span class="keyword">super</span><span>.clone();&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;proto;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;深复制&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;Object&nbsp;deepClone()&nbsp;</span><span class="keyword">throws</span><span>&nbsp;IOException,&nbsp;ClassNotFoundException&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;写入当前对象的二进制流&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ByteArrayOutputStream&nbsp;bos&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;ByteArrayOutputStream();&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ObjectOutputStream&nbsp;oos&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;ObjectOutputStream(bos);&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;oos.writeObject(<span class="keyword">this</span><span>);&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;读出二进制流产生的新对象&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ByteArrayInputStream&nbsp;bis&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;ByteArrayInputStream(bos.toByteArray());&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ObjectInputStream&nbsp;ois&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;ObjectInputStream(bis);&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;ois.readObject();&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;String&nbsp;getString()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;string;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">void</span><span>&nbsp;setString(String&nbsp;string)&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">this</span><span>.string&nbsp;=&nbsp;string;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;SerializableObject&nbsp;getObj()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;obj;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">void</span><span>&nbsp;setObj(SerializableObject&nbsp;obj)&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">this</span><span>.obj&nbsp;=&nbsp;obj;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span><span class="keyword">class</span><span>&nbsp;SerializableObject&nbsp;</span><span class="keyword">implements</span><span>&nbsp;Serializable&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;</span><span class="keyword">final</span><span>&nbsp;</span><span class="keyword">long</span><span>&nbsp;serialVersionUID&nbsp;=&nbsp;1L;&nbsp;&nbsp;</span></span></li><li class=""><span>}&nbsp;&nbsp;</span></li></ol>
<br />
<br />
7种结构型模式<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354192484_5322.PNG' /><br />
6、适配器模式（Adapter）<br />
类的适配器模式<br />
核心思想就是：有一个Source类，拥有一个方法，待适配，目标接口时Targetable，通过Adapter类，将Source的功能扩展到Targetable里<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354187872_4972.PNG' /><br />
对象的适配器模式<br />
基本思路和类的适配器模式相同，只是将Adapter类作修改，这次不继承Source类，而是持有Source类的实例，以达到解决兼容性的问题。<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354188530_8387.PNG' /><br />
接口的适配器模式<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354191586_2062.PNG' /><br />
<p> 讲了这么多，总结一下三种适配器模式的应用场景：</p><br />
<p>类的适配器模式：当希望将一个类转换成满足另一个新接口的类时，可以使用类的适配器模式，创建一个新类，继承原有的类，实现新的接口即可。</p><br />
<p>对象的适配器模式：当希望将一个对象转换成满足另一个新接口的对象时，可以创建一个Wrapper类，持有原类的一个实例，在Wrapper类的方法中，调用实例的方法就行。</p><br />
<p>接口的适配器模式：当不希望实现一个接口中所有的方法时，可以创建一个抽象类Wrapper，实现所有方法，我们写别的类的时候，继承抽象类即可。</p><br />
7、装饰模式（Decorator）<br />
<p>顾名思义，装饰模式就是给一个对象增加一些新的功能，而且是动态的，要求装饰对象和被装饰对象实现同一个接口，装饰对象持有被装饰对象的实例，关系图如下：</p><br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354196367_3730.PNG'/><br />
装饰器模式的应用场景：<br />
1、需要扩展一个类的功能。<br />
2、动态的为一个对象增加功能，而且还能动态撤销。（继承不能做到这一点，继承的功能是静态的，不能动态增删。）
缺点：产生过多相似的对象，不易排错！<br />
8、代理模式（Proxy）<br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354197582_1664.PNG' /><br />
代理模式的应用场景：<br />
如果已有的方法在使用的时候需要对原有的方法进行改进，此时有两种办法：<br />
1、修改原有的方法来适应。这样违反了“对扩展开放，对修改关闭”的原则。<br />
2、就是采用一个代理类调用原有的方法，且对产生的结果进行控制。这种方法就是代理模式。使用代理模式，可以将功能划分的更加清晰，有助于后期维护！<br />
9、外观模式（Facade）<br />
<p>外观模式是为了解决类与类之间的依赖关系的，像spring一样，可以将类和类之间的关系配置到配置文件中，而外观模式就是将他们的关系放在一个Facade类中，降低了类类之间的耦合度，该模式中没有涉及到接口，看下类图：（我们以一个计算机的启动过程为例）</p><br />
<img src='http://img.my.csdn.net/uploads/201211/29/1354200158_3667.PNG' /><br />
<p>如果我们没有Computer类，那么，CPU、Memory、Disk他们之间将会相互持有实例，产生关系，这样会造成严重的依赖，修改一个类，可能会带来其他类的修改，这不是我们想要看到的，有了Computer类，他们之间的关系被放在了Computer类里，这样就起到了解耦的作用，这，就是外观模式！</p><br />
10、桥接模式（Bridge）<br />
<p>桥接模式就是把事物和其具体实现分开，使他们可以各自独立的变化。桥接的用意是：将抽象化与实现化解耦，使得二者可以独立变化，像我们常用的JDBC桥DriverManager一样，JDBC进行连接数据库的时候，在各个数据库之间进行切换，基本不需要动太多的代码，甚至丝毫不用动，原因就是JDBC提供统一接口，每个数据库提供各自的实现，用一个叫做数据库驱动的程序来桥接就行了。我们来看看关系图：</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354241751_5582.PNG' /><br />
<p>这样，就通过对Bridge类的调用，实现了对接口Sourceable的实现类SourceSub1和SourceSub2的调用。接下来我再画个图，大家就应该明白了，因为这个图是我们JDBC连接的原理，有数据库学习基础的，一结合就都懂了。</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354242717_1732.PNG' /><br />
11、组合模式（Composite）<br />
组合模式有时又叫部分-整体模式在处理类似树形结构的问题时比较方便，看看关系图：<br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354243465_5968.PNG' /><br />
<p>使用场景：将多个对象组合在一起进行操作，常用于表示树形结构中，例如二叉树，数等。</p><brr />
12、享元模式（Flyweight）<br />
<p>享元模式的主要目的是实现对象的共享，即共享池，当系统中对象多的时候可以减少内存的开销，通常与工厂模式一起使用。</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354257773_2727.PNG' /><br />
<p>FlyWeightFactory负责创建和管理享元单元，当一个客户端请求时，工厂需要检查当前对象池中是否有符合条件的对象，如果有，就返回已经存在的对象，如果没有，则创建一个新对象，FlyWeight是超类。一提到共享池，我们很容易联想到Java里面的JDBC连接池，想想每个连接的特点，我们不难总结出：适用于作共享的一些个对象，他们有一些共有的属性，就拿数据库连接池来说，url、driverClassName、username、password及dbname，这些属性对于每个连接来说都是一样的，所以就适合用享元模式来处理，建一个工厂类，将上述类似属性作为内部数据，其它的作为外部数据，在方法调用时，当做参数传进来，这样就节省了空间，减少了实例的数量。</p><br />
看个例子：<br />
<ol start="1" class="dp-j"><li class="alt"><span><span class="keyword">public</span><span>&nbsp;</span><span class="keyword">class</span><span>&nbsp;ConnectionPool&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;Vector&lt;Connection&gt;&nbsp;pool;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*公有属性*/</span><span>&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;String&nbsp;url&nbsp;=&nbsp;</span><span class="string">"jdbc:mysql://localhost:3306/test"</span><span>;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;String&nbsp;username&nbsp;=&nbsp;</span><span class="string">"root"</span><span>;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;String&nbsp;password&nbsp;=&nbsp;</span><span class="string">"root"</span><span>;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;String&nbsp;driverClassName&nbsp;=&nbsp;</span><span class="string">"com.mysql.jdbc.Driver"</span><span>;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">int</span><span>&nbsp;poolSize&nbsp;=&nbsp;</span><span class="number">100</span><span>;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;</span><span class="keyword">static</span><span>&nbsp;ConnectionPool&nbsp;instance&nbsp;=&nbsp;</span><span class="keyword">null</span><span>;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;Connection&nbsp;conn&nbsp;=&nbsp;<span class="keyword">null</span><span>;&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*构造方法，做一些初始化工作*/</span><span>&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">private</span><span>&nbsp;ConnectionPool()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pool&nbsp;=&nbsp;<span class="keyword">new</span><span>&nbsp;Vector&lt;Connection&gt;(poolSize);&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">for</span><span>&nbsp;(</span><span class="keyword">int</span><span>&nbsp;i&nbsp;=&nbsp;</span><span class="number">0</span><span>;&nbsp;i&nbsp;&lt;&nbsp;poolSize;&nbsp;i++)&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">try</span><span>&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Class.forName(driverClassName);&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;conn&nbsp;=&nbsp;DriverManager.getConnection(url,&nbsp;username,&nbsp;password);&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pool.add(conn);&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span class="keyword">catch</span><span>&nbsp;(ClassNotFoundException&nbsp;e)&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.printStackTrace();&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span class="keyword">catch</span><span>&nbsp;(SQLException&nbsp;e)&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.printStackTrace();&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;返回连接到连接池&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">synchronized</span><span>&nbsp;</span><span class="keyword">void</span><span>&nbsp;release()&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pool.add(conn);&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="comment">/*&nbsp;返回连接池中的一个数据库连接&nbsp;*/</span><span>&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">public</span><span>&nbsp;</span><span class="keyword">synchronized</span><span>&nbsp;Connection&nbsp;getConnection()&nbsp;{&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">if</span><span>&nbsp;(pool.size()&nbsp;&gt;&nbsp;</span><span class="number">0</span><span>)&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Connection&nbsp;conn&nbsp;=&nbsp;pool.get(<span class="number">0</span><span>);&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pool.remove(conn);&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;conn;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span class="keyword">else</span><span>&nbsp;{&nbsp;&nbsp;</span></span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">return</span><span>&nbsp;</span><span class="keyword">null</span><span>;&nbsp;&nbsp;</span></span></li><li class="alt"><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class=""><span>&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;&nbsp;</span></li><li class="alt"><span>}&nbsp;&nbsp;</span></li></ol>
<br />
通过连接池的管理，实现了数据库连接的共享，不需要每一次都重新创建连接，节省了数据库重新创建的开销，提升了系统的性能！<br />
<br />
<p>行为型模式，共11种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。</p><br />
<p>先来张图，看看这11中模式的关系：</p><br />
<p>第一类：通过父类与子类的关系进行实现。第二类：两个类之间。第三类：类的状态。第四类：通过中间类</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354264672_7575.PNG' /><br />
13、策略模式（strategy）<br />
<p>策略模式定义了一系列算法，并将每个算法封装起来，使他们可以相互替换，且算法的变化不会影响到使用算法的客户。需要设计一个接口，为一系列实现类提供统一的方法，多个实现类实现该接口，设计一个抽象类（可有可无，属于辅助类），提供辅助函数，关系图如下：</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354268408_3835.PNG' /><br />
图中ICalculator提供同意的方法，<br />
AbstractCalculator是辅助类，提供辅助方法，接下来，依次实现下每个类：<br />
首先统一接口：<br />
<p>策略模式的决定权在用户，系统本身提供不同算法的实现，新增或者删除算法，对各种算法做封装。因此，策略模式多用在算法决策系统中，外部用户只需要决定用哪个算法即可。</p><br />
14、模板方法模式（Template Method）<br />
<p>解释一下模板方法模式，就是指：一个抽象类中，有一个主方法，再定义1...n个方法，可以是抽象的，也可以是实际的方法，定义一个类，继承该抽象类，重写抽象方法，通过调用抽象类，实现对子类的调用，先看个关系图：</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354283441_1858.PNG' /><br />
15、观察者模式（Observer）<br />
<p>包括这个模式在内的接下来的四个模式，都是类和类之间的关系，不涉及到继承，学的时候应该 记得归纳，记得本文最开始的那个图。观察者模式很好理解，类似于邮件订阅和RSS订阅，当我们浏览一些博客或wiki时，经常会看到RSS图标，就这的意思是，当你订阅了该文章，如果后续有更新，会及时通知你。其实，简单来讲就一句话：当一个对象变化时，其它依赖该对象的对象都会收到通知，并且随着变化！对象之间是一种一对多的关系。先来看看关系图：</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354285683_8317.PNG' /><br />
16、迭代子模式（Iterator）<br />
<p>顾名思义，迭代器模式就是顺序访问聚集中的对象，一般来说，集合中非常常见，如果对集合类比较熟悉的话，理解本模式会十分轻松。这句话包含两层意思：一是需要遍历的对象，即聚集对象，二是迭代器对象，用于对聚集对象进行遍历访问。我们看下关系图：</p><br />
<img src='http://img.my.csdn.net/uploads/201211/30/1354289861_5945.PNG' /><br />
17、责任链模式（Chain of Responsibility）<br />
<p>接下来我们将要谈谈责任链模式，有多个对象，每个对象持有对下一个对象的引用，这样就会形成一条链，请求在这条链上传递，直到某一对象决定处理该请求。但是发出者并不清楚到底最终那个对象会处理该请求，所以，责任链模式可以实现，在隐瞒客户端的情况下，对系统进行动态的调整。先看看关系图：</p><br />
<img src='http://img.my.csdn.net/uploads/201212/01/1354294176_6016.PNG' /><br />
18、命令模式（Command）<br />
<p>命令模式很好理解，举个例子，司令员下令让士兵去干件事情，从整个事情的角度来考虑，司令员的作用是，发出口令，口令经过传递，传到了士兵耳朵里，士兵去执行。这个过程好在，三者相互解耦，任何一方都不用去依赖其他人，只需要做好自己的事儿就行，司令员要的是结果，不会去关注到底士兵是怎么实现的。我们看看关系图：</p><br />
<img src='http://img.my.csdn.net/uploads/201212/01/1354297121_8890.PNG' /><br />
<p>Invoker是调用者（司令员），Receiver是被调用者（士兵），MyCommand是命令，实现了Command接口，持有接收对象。</p><br />
<p>这个很哈理解，命令模式的目的就是达到命令的发出者和执行者之间解耦，实现请求和执行分开，熟悉Struts的同学应该知道，Struts其实就是一种将请求和呈现分离的技术，其中必然涉及命令模式的思想！</p><br />
19、备忘录模式（Memento）<br />
<p>主要目的是保存一个对象的某个状态，以便在适当的时候恢复对象，个人觉得叫备份模式更形象些，通俗的讲下：假设有原始类A，A中有各种属性，A可以决定需要备份的属性，备忘录类B是用来存储A的一些内部状态，类C呢，就是一个用来存储备忘录的，且只能存储，不能修改等操作。做个图来分析一下：</p><br />
<img src='http://img.my.csdn.net/uploads/201212/01/1354329495_6012.PNG' /><br />
20、状态模式（State）<br />
<p>核心思想就是：当对象的状态改变时，同时改变其行为，很好理解！就拿QQ来说，有几种状态，在线、隐身、忙碌等，每个状态对应不同的操作，而且你的好友也能看到你的状态，所以，状态模式就两点：1、可以通过改变状态来获得不同的行为。2、你的好友能同时看到你的变化。看图：</p><br />
<img src='http://img.my.csdn.net/uploads/201212/01/1354367681_4639.PNG' /><br />
<p>根据这个特性，状态模式在日常开发中用的挺多的，尤其是做网站的时候，我们有时希望根据对象的某一属性，区别开他们的一些功能，比如说简单的权限控制等。</p><br />
21、访问者模式（Visitor）<br />
<p>访问者模式把数据结构和作用于结构上的操作解耦合，使得操作集合可相对自由地演化。访问者模式适用于数据结构相对稳定算法又易变化的系统。因为访问者模式使得算法操作增加变得容易。若系统数据结构对象易于变化，经常有新的数据对象增加进来，则不适合使用访问者模式。访问者模式的优点是增加操作很容易，因为增加操作意味着增加新的访问者。访问者模式将有关行为集中到一个访问者对象中，其改变不影响系统数据结构。其缺点就是增加新的数据结构很困难。</p><br />
<p>简单来说，访问者模式就是一种分离对象数据结构与行为的方法，通过这种分离，可达到为一个被访问者动态添加新的操作而无需做其它的修改的效果。简单关系图：</p><br />
<img src='http://img.my.csdn.net/uploads/201212/01/1354372253_7681.PNG' /><br />
<p>该模式适用场景：如果我们想为一个现有的类增加新功能，不得不考虑几个事情：1、新功能会不会与现有功能出现兼容性问题？2、以后会不会再需要添加？3、如果类不允许修改代码怎么办？面对这些问题，最好的解决方法就是使用访问者模式，访问者模式适用于数据结构相对稳定的系统，把数据结构和算法解耦。</p><br />
22、中介者模式（Mediator）<br />
<p>中介者模式也是用来降低类类之间的耦合的，因为如果类类之间有依赖关系的话，不利于功能的拓展和维护，因为只要修改一个对象，其它关联的对象都得进行修改。如果使用中介者模式，只需关心和Mediator类的关系，具体类类之间的关系及调度交给Mediator就行，这有点像spring容器的作用。先看看图：</p><br />
<img src='http://img.my.csdn.net/uploads/201212/01/1354375826_1485.PNG' /><br />
23、解释器模式（Interpreter）<br />
<p>解释器模式是我们暂时的最后一讲，一般主要应用在OOP开发中的编译器的开发中，所以适用面比较窄。</p><br />
<img src='http://img.my.csdn.net/uploads/201212/02/1354377970_2591.PNG' /><br />
<p>基本就这样，解释器模式用来做各种各样的解释器，如正则表达式等的解释器等等！</p><br />
