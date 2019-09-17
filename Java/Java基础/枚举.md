# 枚举

```
枚举定义格式：
enum 枚举名{ 枚举值表 };
```

枚举关键字（enum）定义的类都继承于枚举类（Enum）



------



### 类集对枚举的支持

#### EnumMap

EnumMap是Map接口的子类，操作形式与Map一致。

可以通过调用EnumMap的方法来实现对于对象的控制。

```
使用EnumMap操作类：

enum Color{
RED,GREEN,BLUE;
}

EnumMap<Color,String> em = new EnumMap<Color,String>(Color.class);
em.put(Color.RED,"红色");
em.put(Color.GREEN,"绿色");
em.put(Color.BLUE,"蓝色");
for(Map.Entry<Color,String>me : em.entrySet()){
	System.out.println(me.getKey()+"-->"+me.getValue())
}
```

#### EnumSet

EnumSet是Set接口的子类，但是在此类中并没有任何的构造方法定义，表示构造方法被私有化。

同时，所有对于此类的方法的操作均是静态操作。

```
测试EnumSet的静态方法：

enum Color{
RED,GREEN,BLUE;
}

EnumSet<Color> es = new EnumSet.allOf(Color.class);	//表示将全部内容设置到集合
/*
	EnumSet<Color> es = new EnumSet.noneOf(Color.class);	//表示此类型的空集合
*/
Iterator<Color> it = es.iterator();
while(it.hasNext()){
System.out.println(it.next());
}
```



------



### 枚举的构造方法

在枚举中可以直接定义构造方法，但一旦构造方法定义之后，则所有的枚举对象都必须明确地调用此构造方法。

```
定义枚举的构造方法：
public enum Color{
	RED("红色"),GREEN("绿色"),BLUE("蓝色");
	private String name;
	Color(String name){
		this.name=name;
	}
	public void setName(String name){
		this.name=name;
	}
	public String getName(){
		return name;
	}
}
```



------



### 枚举的接口

当一个枚举实现一个接口之后，各个枚举对象都必须分别实现接口中的抽象方法。

```
public interface info{
	public String getColor();
}
public enum Color implements info{
	RED{
		public String getColor(){return "红色";}
	},
	GREEN{
		public String getColor(){return "绿色";}
	},
	BLUE{
		public String getColor(){return "蓝色";}
	};
}
```



------



#### 枚举中的抽象方法

在一个枚举中裤直接定义一个或者多个抽象方法。

注:枚举中的每个对象都必须单独地实现这些抽象方法。

```
public enum Color{
	RED{
		public String getColor(){return "红色";}
	},
	GREEN{
		public String getColor(){return "绿色";}
	},
	BLUE{
		public String getColor(){return "蓝色";}
	};
	public abstract String getColor();
}
```

