# Interface (Arayüz)

Arayüzler yapı olarak **`soyut sınıflara`** benzer. Soyut sınıflarda, gövdesiz soyut metotları ve tanımlayabileceğimiz diğer metotları kullanabiliyorduk ancak interface'lerde bütün metotlar **gövdesiz** olarak tanımlanır. Bu arayüzü uygulayan sınıflar **abstract** değilse bu metotların tamamını **override** etmek zorundadır. Bu nedenle arayüzlerde, soyut metot tanımlarken **`abstract`** anahtar kelimesini kullanmaya gerek yoktur.

**`Not:`** Java 8 - 9 ile gelen **`default`**, **`private`** ve **`static`** anahtar kelimeleri yardımıyla metotlara gövde ekleyebiliyoruz.

Interface'ler içinde tanımlı olan metotlar diğer sınıflar için **`şartname`** (specification) niteliği taşır. Yani bir işin nasıl yapılacağı değil, işin yaparken hangi adımları veya ne yapması gerektiğini tanımlar. Arayüzlerin sınıfları birleştirici özelliği vardır ve temelde çoklu kalıtımı basite indirgemek için oluşturulmuştur. Kod yapısı sınıf tanımlamaya benzer. Sınıflar, kullanmak istediği arayüzleri **implements** anahtar sözcüğü ile kendilerine dahil eder. 

```java
accessModifier interface <interface-name>{
    // metotlar ve değişkenler
}
```

Arayüz içinde tanımlı olan değişkenlerin erişim belirteçleri **public static final** tipindedir ve ilk değer ataması zorunludur, metotlar ise **public**'dir. Arayüz içinde tanımlı olan değişkenler diğer sınıflarda daha çok sabit olarak kullanılacağından, bu değerleri değiştirmek mümkün değildir.

Sınıflar sadece bir adet soyut sınıfı miras alabilirken, birden çok arayüzü bünyesinde barındırabilir. Bu da çoklu kalıtım işini kolaylaştırır.

Arayüzlerde, soyut sınıflarda olduğu gibi bir **ilişki** kavramı yoktur. Yani arayüz ve bunu kullanan sınıflar arasında **kalıtım** açısından bir bağlantı olmayabilir. 

**`Not:`** Bir arayüz içinde aynı isimde iki metot varsa, bu metotların aldığı parametrelerin farklı olması gerekir. Dönüş tiplerinin farklı olması bir anlam ifade etmez, **hata** oluşur. Bu durum, metotlardaki **overloding** işlemine benzer. 


```java
public interface Language {
    void getName(String name);
}
```

```java
public class ProgrammingLanguage implements Language {
    public void getName(String name) {
        System.out.println("Programming Language: " + name);
    }
}
```

```java
public class Driver {
    public static void main(String[] args) {
        ProgrammingLanguage language = new ProgrammingLanguage();
        language.getName("Java");
    }
}
```
Output:

```
Programming Language: Java
```

<br>

## Interface'lerin İmplementasyonu 

Soyut sınıflarda olduğu gibi arayüzlerle de nesne oluşturulamaz, dolayısıyla içinde **constructor** barındırmaz ancak daha önce bahsedildiği gibi bir sınıf aracılığıyla bu interface'leri **uygulayabiliriz**.  Bunun dışında arayüzlerin referans tutucu özelliği vardır. Yani bir arayüz değişkeni kendisini **implemente eden** bir sınıfın nesnesini işaret edebilir ([polimorfizm](https://github.com/barisdalyan/java-notes/blob/master/content/polymorphism/polymorphism_tr.md#isinstance-%C3%B6rne%C4%9Fi)). Bu özellik sınıfları  gruplamak için kullanılabilir, bu amaçla kullanılacak arayüzlerin (**tagging interfaces**) içinde override edilecek metotlar yoktur.

```java
public interface Polygon {
    void getArea(int length, int width);
}
```

```java
public class RightTriangle implements Polygon {
    public void getArea(int length, int width) {
        System.out.println("The area of the right triangle: " + (length * width) / 2);
    }
}
```

```java
public class Driver {  
    public static void main(String[] args) {  
  
        Polygon triangle = new RightTriangle();  
        triangle.getArea(5, 6);  
  
   /*   
       'triangle' değişkeni ile sadece Polygon arayüzünden override edilen   
       metotlara ulaşılabilir. RightTriangle sınıfının kendi (override edilmeyen)   
       metotlarına ulaşılamaz. Tüm metotlara erişmek için:  
       
       Not: Access modifiers ile erişimi kısıtlananlar hariç.  
       
       RightTriangle rightTriangle = new RightTriangle();  
       rightTriangle.getArea(5, 6);   */  
  
  }  
}
```

Output:
```
The area of the right triangle: 15
```

**`Not:`** C sınıfı birden çok interface'i implemente edebilir.

```java
interface A {
    // A'nın üyeleri
}

interface B {
    // B'nin üyeleri
}

class C implements A, B {
    // A'nın soyut üyeleri
    // B'nin soyut üyeleri
}
```

<br>

## Interface'leri Genişletme

Arayüzlerde genişletme, başka bir arayüzün bu arayüzü **miras** alması ile mümkün olur. Kalıtım, sınıflardaki gibi **extends** anahtar sözcüğü ile gerçekleşir. Bir sınıf, bir arayüzü implemente ediliyorsa ve bu arayüz de başka bir arayüzden miras alınmışsa, sınıfımız her iki arayüzdeki metotları **override** etmelidir. Bir arayüz **birden çok** arayüzü genişletebilir.

```java
interface A {
   ...
}
interface B {
   ... 
}

interface C extends A, B {
   ...
}
```

<br>

## Interface İçinde Başka Bir Interface Kullanma

Bir arayüz başka bir arayüz içinde bulunabilir. Dahili arayüzler varsayılan olarak **public static** olduğu için tekrar tanımlamaya gerek yoktur.

```java
public interface Arayuz1 {
    void method1();

    interface Arayuz2 {
        void method2();
    }
}

public interface Arayuz3 {
    void method3();
}
```

```java
public class A implements Arayuz1 {
    @Override
    public void method1() {
        System.out.println("Arayüz1'deki method1 override edildi.");
    }
}

public class B implements Arayuz1.Arayuz2 {
    @Override
    public void method2() {
        System.out.println("Arayüz2'deki method2 override edildi.");
    }
}

public class C implements Arayuz3 {
    @Override
    public void method3() {
        System.out.println("Arayüz3'deki method3 override edildi.");
    }
}
```

```java
public class Driver {
    public static void main(String[] args) {
        A o1 = new A();
        o1.method1();
        B o2 = new B();
        o2.method2();
        C o3 = new C();
        o3.method3();
    }
}
```

Output:
```
Arayüz1'deki method1 override edildi.
Arayüz2'deki method2 override edildi.
Arayüz3'deki method3 override edildi.
```

<br>

## Java Interface'lerde default Metotlar

Java 8 sürümü ile artık arayüzlere metotlar ekleyebiliyoruz. Bunu yapabilmek için **`default`** anahtar kelimesini kullanmamız gerekiyor. Bu metotlar diğer metotlar gibi miras alınabilir ve isteğe bağlı ezilebilir (**overriding**).

```java
interface <interface-name> {
 default void method() {
   // artık gövde kısmı da tanımlanabiliyor
  }
}
```
**`Senaryo:`** Yeni çalışan işe alınır ancak CV'sinde aksini kanıtlamadığı sürece, junior muamelesi görür. 


```java
enum Developer {
    JUNIOR(5000), MID(10_000), SENIOR(16_000);

    private int salary;

    Developer(int salary) {
        this.salary = salary;
    }

    public int getSalary() {
        return salary;
    }
}
```

```java
public interface Accounting {  
    void printInfo();  
  
    default void countSalary() {  
        System.out.println("Salary for Junior Developer: " + "$" + Developer.JUNIOR.getSalary() + "\n");  
    }  
}
```

```java
public class Person implements Accounting {  
    private int id;  
    private String name;  
  
    @Override  
    public void printInfo() {  
        System.out.println("Employee ID: " + id);  
        System.out.println("Name: " + name);  
        countSalary();  
    }  
  
    public int getId() {  
        return id;  
    }  
  
    public void setId(int id) {  
        this.id = id;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
}
```

```java
public class SeniorDev extends Person {  
    public SeniorDev(int id, String name) {  
        setId(id);  
        setName(name);  
        printInfo();  
    }  
  
    @Override  
    public void countSalary() {  
        System.out.println("Salary for Senior Developer: " + "$" + Developer.SENIOR.getSalary() + "\n");  
    }  
  
    @Override  
    public void printInfo() {  
        System.out.println("Employee ID: " + getId());  
        System.out.println("Name: " + getName());  
        countSalary();  
    }  
}
```

```java
public class JuniorDev extends Person {  
    public JuniorDev(int id, String name) {  
        setId(id);  
        setName(name);  
        printInfo();  
    }  
}
```

```java
public class Driver {  
    public static void main(String[] args) {  
        Person dev1 = new SeniorDev(265, "James");  
        Person dev2 = new JuniorDev(267, "Ellie");  
    }  
}
```

Output:
```
Employee ID: 265
Name: James
Salary for Senior Developer: $16000

Employee ID: 267
Name: Ellie
Salary for Junior Developer: $5000
```
Yukarıdaki örnekte **SeniorDev** sınıfı countSalary() metodunu **ezerek** (by overriding) enum sınıfından yeni bir sabit yazdırdı ancak **JuniorDev** sınıfında default metot çağırıldı. 

<br>

## Java Interface'lerde private - static - private static Metotlar

Java 8 ile gelen diğer bir yenilikle artık interface'lerin içinde **static** metotlar tanımlanabiliyor. Sınıflarda olduğu gibi, bu metotlara interface referansı ile de ulaşmak mümkün. 


```java
interface <interface-name> {
    static void method(){
        System.out.println("Arayüz içindeki static method.");
    }
}

// bir sınıf metodundan static metot bu şekilde çağrılabilir
 <interface-name>.method();
```
**`Not:`** Java 9 sürümüyle birlikte **private** ve **private static** metotlar da interface'ler içinde desteklenmektedir. Bu metotlar arayüz içindeki kod tekrarını engellemek için kullanılır. ``private`` metotlar sadece bu arayüz içinde kullanılır, başka bir interface veya sınıftan bu metotlara ulaşamayız (miras alınamaz). 

```java
interface <interface-name> {
   private static void methodName() {
      ...
   }
   private void methodName() {
      ...
   }
}
```

```java
public interface InterfaceExample {
    void abstractMethod();

    default void defaultMethod() {
        privateMethod();
        privateStaticMethod();
        System.out.println("> Inside default method");
    }

    static void staticMethod() {
        privateStaticMethod();
        System.out.println("> Inside static method");
    }

    private void privateMethod() {
        System.out.println("> Inside private method");
    }

    private static void privateStaticMethod() {
        System.out.println("> Inside private static method");
    }
}
```

```java
public class PrivateStaticMethodTest implements InterfaceExample {
    @Override
    public void abstractMethod() {
        System.out.println("> Inside abstract method");
    }
}
```

```java
public class Driver {
    public static void main(String[] args) {
        InterfaceExample instance = new PrivateStaticMethodTest();
        instance.abstractMethod();
        instance.defaultMethod();
        InterfaceExample.staticMethod();
    }
}
```

Output:
```
> Inside abstract method
> Inside private method
> Inside private static method
> Inside default method
> Inside private static method
> Inside static method
```
