# Gang of Four's 23 design pattern
设计模式
---
1. 创建型模式
   1. **工厂模式** 
      1. `简单工厂：用一个工厂类创造对象实例，不关心具体实现`
      2. 分为普通 -> 多方法 -> 和静态方法简单工厂 `用一个produce方法 -> 把produce方法解耦成多方法 -> 把解耦开的produce方法用静态方法实现`
      3. 简单工厂中，工厂类集成了所以实例的创建逻辑，违反开闭原则
      4. `工厂模式：父类提供创建产品对象的公共接口，子类复杂生产具体的产品对象`
      5. 即工厂模式的每个子类是一个简单工厂
   2. **抽象工厂模式**
      1. ``接口声明创建各种抽象方法的产品``
      2. ```mermaid
            graph LR;
               客户端 --> 抽象工厂
               具体产品-.->客户端
               抽象工厂--> 具体工厂1 & 具体工厂2 & 抽象产品1 & 抽象产品2
               subgraph 抽象产品
               抽象产品1
               抽象产品2
               end

               subgraph 具体工厂
               具体工厂2 --抽象产品1--> 具体产品1.1
               具体工厂2 --抽象产品2--> 具体产品1.2
               具体工厂1 --抽象产品1--> 具体产品2.1
               具体工厂1 --抽象产品2--> 具体产品2.2
               end

         ```
            
   3. **单例模式**
      1. ``一个类只有一个实例，并提供访问该实例的全局节点``
         1. 某个类只有实例
         2. 自行创建这个实例
         3. 自行向整个系统提供这个实例
      2. 控制共享资源
      3. 构造方法
      ```mermaid
         graph LR
            多进程锁-->method
            default(将默认构造方法设为私有)-->method(新建一个构造方法)--调用私有构造方法-->创建对象-->save(保存在静态成员变量中)
            default -.-> 创建对象
            save--静态调用方法-->client(客户端)
      ```
      4. 缺点
         1. 违反单一职责原则（解决了2个问题）
         2. 掩盖各组件了解过多等不良设计
         3. 难以测试
         4. 多线程需要特殊处理
   
   4. **建造者模式**
      1. ``将复杂对象的构建和表示分离，分步骤创建复杂对象``
      2. 用相同的创建代码生产不同类型和形式的对象
      3. 可以将生成器步骤抽象成主管类
   5. **原型模式**
      1. ``复制已有对象，有不需要使对象依赖他们所属的类``
      2. 实现一个原型接口
      3. 一般在直接创造对象代价大时使用
      4. 预生成原型甚至可以代替子类的构造
2. **结构型模式**
   1. **适配器模式** ``Adapter Pattern``
      1. ``Wrapper 使接口不兼容的对象能够相互合作``
      2. 实现其中一个对象的接口，并对另一个对象进行封装
      3. 类适配器：直接继承两个对象的接口（多重继承c++）
      4. ```mermaid
         graph LR;
            不便修改的不兼容第三方服务端-->适配器-->客户端
   2. **桥接模式**
      3. ``将一个大类或一系列联系紧密的类拆分成抽象和实现两个独立的层次结构，从而分开使用``
   4. **过滤器模式**
   5.  **组合模式**
       1.  ``将对象组合成树状结构，并能像使用独立对象一样使用呢他们``
       2.  创造一个保护自己对象组的类，该类提供修改相同对象组的方法
       3. 构造方法
         ```mermaid
            graph LR
               客户端 --> 容器-->容器 & 叶节点
               叶节点 --组件--> 执行
               组件--提供接口-->简单项目和复杂项目的共有操作
         ```
       4. 叶节点是简单元素，不包含子项目
       5. 容器是复杂元素，含有添加和删除子元素的方法，并同时保存叶节点和容器

   6.  **装饰器模式**
   7.  **外观模式**
   8.  **享元模式**
   9.  **代理模式**
3.  **行为型模式**
    1.  **责任链模式**
    2.  **命令模式**
    3.  **解释器模式**
    4.  **迭代器模式**
    5.  **中介者模式**
    6.  **备忘录模式**
    7.  **观察者模式**
    8.  **状态模式**
    9.  **空对象模式**
    10. **策略模式**
    11. **模板模式**
    12. **访问者模式**
4.  **J2EE模式**
    1.  **MVC模式**
    2.  **业务代表模式**
    3.  **组合实体模式**
    4.  **数据访问对象模式**
    5.  **前端控制器模式**
    6.  **拦截过滤器模式**
    7.  **服务定位器模式**
    8.  **传输对象模式**

设计原则--**低耦合，高内聚**
---
1. 开闭原则 
   1. ``对扩展开放，对修改关闭``
   2. ``接口和抽象类``
2. 里氏代换原则（LSP ``Liskov Substitution Principle``）
   1. ``任何基类可以出现的地方，子类一定可以出现``
      1. 子类可以实现父类的抽象方法，但不能覆盖父类的非抽象方法
      2. 子类可以有自己的个性
      3. 输入参数可以被放大
      4. 输出参数可以被缩小
   2. 尽量从抽象类继承
   3. 如果B继承A违反LSP
      1. 利用C作为一个超类，将共同行为移到C
      2. 继承改为委派关系
3. 依赖倒转原则
   1. ``针对接口编程，依赖抽象而不依赖具体``
   2. 高层模块不应该依赖低层模块，二者都应该依赖抽象
   3. 抽象不应该依赖细节，细节应该依赖抽象
4. 接口隔离原则
   1. ``采用多个与特定客户类有关的接口，比采用一个通用接口好``
   2. 客户端不应该依赖它不需要的接口
   3. 类间的关系应该建立在最小接口上
5. 迪米特法则
   1. ``一个对象应该对其他对象有最少的了解``
   2. 只与直接的朋友通信
   3. 但不要过度创建中介
6. 合成复用原则（类有三种关系：关联、泛化（继承）、依赖）
   1. ``尽量采用组合（contains-a）、聚合（has-a）的方式而不是继承（is-a）的方式来达到软件复用``
   2. 继承是白箱复用，父类对子类是透明的，这破坏了类的封装性
   3. 关联（单向或双向）
      1. 复合是``引用``的聚合，弱的拥有，部分的生命周期甚至可能大于整体
      2. 合成是``值``的聚合，强的拥有，整体完全支配部分，部分不能脱离整体存在
   4. 耦合性排序``合成 <聚合< 组合<继承``
7. 单一职责原则
   1. ``一个类只负责一个职责``



 
