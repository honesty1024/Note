# 注解

#### 系统内建的Annotation

@Override：表示进行正确的覆写操作

@Deprecated：表示不建议使用的操作

@SuppressWarnings：表示压制警告

#### 自定义Annotation

```
定义Annotation的语法：
public @interface Annotation的名称{
	//可以定义若干个属性,如下的key、value，可以给属性设置默认内容，如[]
	public String key() [default "ss"];
	public String value();
}
```

#### Retention和RetentionPolicy

Retention本身是一个Annotation，其中的取值是通过RetentionPolicy这个枚举类型指定的范围。

在RetentionPolicy中规定了以下3个作用范围。

（1）只在源代码中起作用：public static final RetentionPolicy SOURCE

（2）只在编译之后的class中起作用：public static final RetentionPolicy CLASS

（3）在运行的时候起作用：public static final RetentionPolicy RUNTIME

如果一个Annotation要想起作用，则必须使用RUNTIME范围。

任何一个自定义的Annotation都是继承了java.lang.annotation.Annotation接口。

在一个自定义的Annotation编写的时候，如果想要让其有意义，则必须使用RUNTIME声明范围。

@Retention(value=RetentionPolicy.RUNTIME)

#### 反射与Annotation

一个Annotation如果要想起作用，则肯定要依靠反射机制。通过反射可以取得在一个方法上声明的Annotation的全部内容。

在Filed、Method、Constructor的父类上定义了以下与Annotation反射操作相关的方法

（1）取得全部的Annotation：public Annotation[] getAnnotations(); 

（2）判断操作的是否是指定的Annotation。

​		public boolean isAnnotationPresent(Class<? extends Annotation>annotationClass);zai 

#### Target

在@Target注释中，存在ElementType类型的变量，在此变量中存在7种范围。

（1）只能在Annotation中出现：public static final ElementType ANNOTATION_TYPE

（2）只能在构造方法中出现：public static final ElementType CONSTRUCTOR

（3）本地变量上使用：public static final ElementType LOCAL_VARIABLE

（4）只能在方法上使用：public static final ElementType METHOD

（5）在参数声明上使用：public static final ElementType PARAMETER

（6）在包的声明上使用：public static final ElementType PACKAGE

（7）只能在类或接口上使用：public static final ElementType TYPE

@Target(value=ElementType.变量)

#### Documented

表示的是文档的注释格式，该注释可以在doc文档中出现

#### Inherited

表示一个Annotation能否被使用其类的子类继续继承下去。如果没有写上此注释，则此Annotation根本就是物防继承的。