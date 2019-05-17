# Java之反射

>反射的基本思路
>>Step1：获得目的类的class字节码对象。

>>Step2：通过getConstructor()获得构造器的方式获得构造器对象。

>>Step3：通过构造器类的方法newInstance()获得所反射的对象。

>>NOTE:通过反射可以获得**成员变量（属性）**、**成员方法**、**构造方法**

##如何获取class字节码对象(三种方式)
>>方式一：通过对象获取
```
    Person p = new Person(); 
    Class clazz = p.getClass();
```
>>方式二：类名获取
```
    Class clazz = Person.class;
```
>>方式三：Class类的静态方法获取
```
    Class clazz = Class.forName("类的全包名");
```
>>**Ps：拿到的class字节码对象具有唯一性。**


##反射获得构造方法
```
    //获得字节码对象
    Class clazz = Class.forName("类的全包名");
    //获得所有公共构造方法(除私有),返回值为构造方法对象数组
    Constructor[] cons = clazz.getConstructors();
    //获得所有构造方法(包括私有)
    Constructor[] cons = clazz.getDeclaredConstructors();  
    //获得指定空参构造方法
    Constructor con = clazz.getConstructor(); 
    //获得指定有参构造方法
    Constructor con = clazz.getConstructor(String.class,int.class); 
    //获得指定有参构造方法(包括私有)
    Constructor con = clazz.getDeclaredConstructor(String.class,int.class); 
    //运行时期，取消java的权限检查——暴力反射
    con.setAccessible(true);
    //通过构造方法实例化对象
    Object obj=con.newInstance();
    Object obj=con.newInstance("你好"，22);
```

##反射获取到成员变量和成员方法
>>NOTE:反射的泛型擦除原理：java是伪泛型，编译后的class文件是没有泛型的，可利用反射绕开泛型。
```
    //获得字节码对象
    Class clazz = Class.forName("类的全包名");
    //通过字节码对象的newInstance()方法创建实例对象——调用的是空参构造。
    Object obj = clazz.newInstance();
    
    //反射获得成员变量：
    Class clazz = Class.forName("类的全包名");
    //获得所有公共的成员变量
    Field[] fields = clazz.getFields();
    //获得所有成员变量(包括私有)
    Field[] fields = clazz.getDeclaredFields();
    Field field = clazz.getField(““方法名”);
    //方法中需要对象的支持，该对象通过c.newInstance()获得反射获得成员方法：
    Field.set(obj,参数);
    Methods[] methods=c.getMethods()；//获取所有公共成员方法，包括继承
    Methods method=c.getMethod(“方法名”，可变参数的class字节码文件，可空参)；
    method.invoke(Object obj,参数)；//同样执行方法也需要对象的支持
    
    
    //返回表示声明该Field字段对象的类或接口的Class字节码对象。
    java.lang.reflect.Field.getDeclaringClass()
    
    //判断调用的a字节码对象是否与参数b字节码对象相等或为其父类或接口
    java.lang.Class.isAssignableFrom()
    
    //获取类的所有字段，包括私有字段
    java.lang.Class.getDeclaredFields()
    
    //返回指定对象上由Field表示的字段的值
    java.lang.reflect.Field.get()
```