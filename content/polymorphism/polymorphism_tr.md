
# Polymorphism (Çok Biçimlilik)

Polimorfizm, **çoklu biçim** veya **çoklu şekil** anlamına gelir. Polimorfizm yapılarak bir nesne referansına, farklı nesneler yüklenebilir. Bu konu **Kalıtım** kavramı ile iç içedir. Dolayısıyla polimorfizm yapabilmek için Kalıtım mantığını bilmek gerekir. Polimorfizm'de aynı varlıklar (metot, operatör veya nesne) farklı senaryolar için farklı işlemler gerçekleştirebilir. 


```java
public class Credit {

    public void getRateOfInterest() {
        System.out.println("Hoşgeldin Kredisi Faiz Oranı: % 1,20");
    }
}

public class ConsumerLoan extends Credit {

   @Override
    public void getRateOfInterest() {
        System.out.println("İhtiyaç Kredisi Faiz Oranı: % 1,90");
    }
}

public class HouseLoan extends Credit {

    @Override
    public void getRateOfInterest() {
        System.out.println("Konut Kredisi Faiz Oranı: % 1,35");
    }
}
```


```java
public class Driver {
    public static void showRates(Credit... creditType) {
        for (Credit show : creditType) {
            show.getRateOfInterest();
        }
    }

    public static void main(String[] args) {

        System.out.println("----- MazeBank Kredi Faizleri -----");
        Credit credit = new Credit();
        ConsumerLoan consumer = new ConsumerLoan();
        HouseLoan house = new HouseLoan();

        showRates(credit, consumer, house);
    }
}
```

Output:

```
----- MazeBank Kredi Faizleri -----
Hoşgeldin Kredisi Faiz Oranı: % 1,20
İhtiyaç Kredisi Faiz Oranı: % 1,90
Konut Kredisi Faiz Oranı: % 1,35
```

- **Neden Polimorfizm?**
Polimorfizm daha tutarlı kod yazmamızı sağlar. Önceki örnekte kredinin türüne göre ``getInterestCustomer`` ve ``getInterestHouse`` gibi iki ayrı metot da yazabilirdik ancak her sınıf için ayrı ayrı yazılan metotlar tutarsızdır ve temiz koddan uzaktır. Bunun yerine ortak bir iş yapan bir metotla daha temiz ve tutarlı bir kod yazmış oluruz.

Java'da polimorfizm iki türe ayrılmıştır:

- Runtime Polymorphism
- Compile Time Polymorphism

## Runtime Polymorphism (Geç Bağlama)

Dynamic Method Dispatch veya Dynamic Binding olarak da bilinir. Runtime Polymorphism, Nesne Yönelimli Programlama'da üst sınıf referansının alt sınıf nesnesini işaret ettiği durumlarda yaygın olarak kullanılır. Referans değişkeni bir **sınf** veya **interface** olabilir. Bu polimorfizmi gerçekleştirmek için metot **overriding** yöntemi kullanılır. Eğer bir alt sınıf nesnesi üst sınıfı miras alıyor ancak üst sınıf metodunu override etmeden kullanmak isterse, JVM çalışma zamanında üst sınıf metodunu çalıştırır. Aksi halde JVM, alt sınıfta override edilen metot içinde **super** anahtar kelimesi kullanılmadıkça çalışma zamanında bu metodu çalıştırır. 


```java
public class LivingBeing { // Superclass
    public void print() {
        System.out.println("Canlı sınıfı");
    }
}

public class Human extends LivingBeing { // Subclass
    @Override
    public void print() {
        System.out.println("İnsan sınıfı");
    }
}

public class Animal extends LivingBeing {
  /*  @Override
    public void print() {
        System.out.println("Hayvan sınıfı");
    }*/
}

public class Plant extends LivingBeing {
    @Override
    public void print() {
        System.out.println("Bitki sınıfı");
    }
}
```


```java
public class Driver {
    public static void getObject(LivingBeing obj) {
        obj.print();
    }

    public static void main(String[] args) {

        LivingBeing living = new LivingBeing();
        Human human = new Human();
        Animal animal = new Animal();
        Plant plant = new Plant();

        getObject(living);
        getObject(human);
        getObject(animal);
        getObject(plant);
    }
}
```

Output:

```java
Canlı sınıfı
İnsan sınıfı
Canlı sınıfı
Bitki sınıfı
```

Bu örnekte ``getObject()`` metodu **LivingBeing** türünde bir parametre alıyor ancak biz bu tipte bir parametreye Human, Animal ve Plant türünde parametreler gönderdik. Derleyici buna **kızmaz** çünkü **yukarı çevrim** yaptık. Argüman sınıflar da LivinBeing sınıfından türemiştir, yani her bitki bir canlıdır veya her insan bir canlıdır. Hayvan sınıfı Canlı sınıfını metodunu override etmediği için JVM runtime'da Canlı (Superclass) metodunu çalıştırdı. Java'da alt sınıflardan oluşturulan nesneler üst sınıf referansına bağlanabiliyor ayrıca **arayüzler** de kendisini **implemente** eden sınıfların nesnelerini tutabilir.

Yukarıdaki örnekte getObject() metodunda yapılan işlem şudur:

```java
   
  LivingBeing obj = new Living();
  LivingBeing obj = new Human(); // --> upcasting (yukarı çevrim)
  LivingBeing obj = new Animal(); // --> upcasting
  LivingBeing obj = new Plant(); // --> upcasting
        
```

**``Not:``** Polimorfizm yaptığımızda hangi nesnenin metodunun çağırılacağı, **çalışma anında** belirlenir çünkü program çalıştığında nesneyi kullanacak olan metoda parametre göndeririz. Derleme anında bu metodun hangi nesneyi kullanacağı belli değildir. Yani JVM, getObject() metodunun Canlı sınıfının print() metodunu mu yoksa İnsan sınıfının print() metodunu mu kullanacağını çalışma anında belirler. Bu duruma **Geç Bağlama** denir. Eğer İnsan sınıfı bu metodu override etmeseydi üst sınıf olan Canlı sınıfının print() metodu çalışacaktı. 

İlgili örnekte Polimorfizm kullanmasaydık getObject() metodunu aşağıdaki gibi de yazabilirdik. Burada, gelen parametrenin hangi sınıfa ait olduğu kontrol edilip **downcasting** (Subclass referans değişkeninin, Superclass nesnesini işaret etmesidir.) ile print() metodu çağırılıyor. **Polimorfizm** ile nesne üzerinde karşılaştırma yapmadan nesnenin referansına göre işlem yapabiliyoruz.

```java

    if (obj instanceof Living){
        Living living = obj; 
        living.print();
    }
    else if (obj instanceof Human){
        Human human = (Human) obj; // downcasting (aşağı çevrim)
        human.print();
    }
    else if (obj instanceof Animal){
        Animal animal = (Animal) obj; // downcasting 
        animal.print();
    }
    else if (obj instanceof Plant){
        Plant plant = (Plant) obj; // downcasting 
        plant.print();
    }
```

``instanceof`` anahtar kelimesinin görevi, nesnelerin ait olduğu (oluşturulduğu) sınıfı kontrol etmektir. Eğer o sınıftan oluşturulmuş veya miras alıyorsa **true** aksi halde **false** döner. **Cast** işlemi, parametredeki tip ile atama yapılacak referansın tipi farklı olduğu için (Canlı referansı Hayvan nesnesinin referansına atanmaya çalışılıyor) yapıldı. Bu konuyu ilgili başlıkta tekrar inceleyeceğiz. 


### Geç Bağlama (Late Binding)

Yukarıdaki metodlara parametre olarak nesne gönderdik ve bu çağırılan metodların hangi nesne üzerinden çağırılacağına Java Sanal Makinesi (JVM) karar verdi. Buna duruma Geç Bağlama demiştik. Yani bağlama işlemi çalışma zamanında belli oluyor. Örnek olarak **rastgele sayılar** üreten bir programımız olsun. Bu rastgele sayılar derleme anında oluşturulmaz. Program çalıştığında zaman sayılar rastgele üretilmeye başlar. Geç Bağlama'da da durum böyledir. Eğer rastgele nesneler üretir ve bu nesneleri de yukarıdakine benzer bir metoda gönderirsek, çağırılan metodun hangi nesne üzerinden çağırılacağı **çalışma zamanında** belli olur.


```java
public class Language {
    public void displayInfo() {
        System.out.println("Common English Language");
    }
}

public class Java extends Language {
    @Override
    public void displayInfo() {
        System.out.println("Java Programming Language");
    }
}

public class Go extends Language {
    @Override
    public void displayInfo() {
        System.out.println("Go Programming Language");
    }
}

public class C extends Language {
    @Override
    public void displayInfo() {
        System.out.println("C Programming Language");
    }
}
```

```java
public class Driver {
    public static void getObject(Language obj) {
        obj.displayInfo();
    }

    public static void main(String[] args) {
        Language[] langs = new Language[3];
        
        for (int i = 0; i < 3; i++) {
            int index = (int) (Math.random() * 3);

            switch (index) {
                case 0:
                    langs[0] = new Java(); // upcasting
                    getObject(langs[0]);
                    break;
                case 1:
                    langs[1] = new Go(); // upcasting
                    getObject(langs[1]);
                    break;

                case 2:
                    langs[2] = new C(); // upcasting
                    getObject(langs[2]);
                    break;
            }
        }
    }
}
```

Output:

```
Go Programming Language
Java Programming Language
C Programming Language
```

**``Not:``** Java'da metot overriding yapılabilirken, **nesne değişkenlerinde** bu işlem gerçekleştirilemediği için runtime polimorfizm bu değişkenler ile elde **edilemez.** 

Aşağıdaki örnekte çalışan yaşını **``21``** olarak beklerken,

```java
public class Person {
    protected int age = 35;
}

public class Employee extends Person {
    protected int age = 21;
}

public class Driver {
    public static void main(String[] args) {
        Person employee = new Employee();
        System.out.println("Çalışan yaşı: " + employee.age); 
        // Output: Çalışan yaşı: 35
    }
}
```

### instanceof ile Tip Kontrolü

Bu anahtar kelime (operatör), nesnelerin **hangi türe** (class, subclass, interface) ait olduğunu bulmaya yardımcı olur.

```java
public class A { public int numberA = 13; }

public class B extends A { public int numberB = 11; }

public class C extends B { public int numberC = 7; }

public class D extends B { public int numberD = 5; }
```

```java
public class Driver {
    public static void main(String[] args) {

        A a1 = new A();
        B b1 = new B();
        C c1 = new C();
        D d1 = new D();

        System.out.println(b1 instanceof B);
        System.out.println(a1 instanceof B);
        System.out.println(c1 instanceof A);
        System.out.println(b1 instanceof C);
        System.out.println(c1 instanceof B);
        System.out.println(d1 instanceof B);
        System.out.println(d1 instanceof A);

        System.out.println("-------------");

        if (c1 instanceof A) {
            System.out.println("c nesnesi A sınıfının elemanına erişebilir: " + c1.numberA);
        } else
            System.out.println("c nesnesi numberA değerine erişemez");

        if (b1 instanceof D)
            System.out.println("b nesnesi D sınıfına erişebilir ");
        else
            System.out.println("b nesnesi D sınıfına erişemez"); 
    }
}
```

Output:

```
true
false
true
false
true
true
true
-------------
c nesnesi A sınıfının elemanına erişebilir: 13
b nesnesi D sınıfına erişemez
```

Örnekteki temel mantık şu şekildedir. D sınıfını B'den, B sınıfını da A'dan türettik. Dolayısıyla D sınıfından oluşturacağımız bir nesne, aynı zamanda A sınıfının da bir örneğidir (instance) ve **private** erişim belirtecine sahip olmayan üyelerine erişebilir. Buna benzer şekilde **downcasting** ile de erişim mümkün olur ancak bunun tersi mümkün değildir. Yani üst sınıf altı sınıfın bir örneği olmadığı için üyelerine **erişemez.**

**``Not:``** Java'da her sınıf **Object** sınıfının birer örneği olduğu için yukarıdaki her sınıf Object sınıfının üyelerine erişebilir. **toString()** metodu buna örnek verilebilir.

**instanceof** anahtar kelimesiyle bir değişkenin ait olduğu sınıfı şu şekilde karşılaştırabiliriz:

```java
public class Comparison{
    public static void main(String[] args) {

        String word = "Java 11";
        Integer number = new Integer(15);

        System.out.println(word instanceof java.lang.String);
        System.out.println(number instanceof java.lang.Integer);
        
        /* Inconvertible types; cannot cast 'java.lang.String' to 'java.lang.Character'
        System.out.println(word instanceof java.lang.Character); */
    }
}
```

Output:

```
true
true
```

Bu operatörü dinamik olarak kullanmak münkün değildir. Yani bir sınıf nesnesini başka bir sınıfla karşılaştırmaya çalıştığımızda, operatör yukarıdaki örnekte olduğu gibi **compile time error** fırlatabilir. Bu operatöre alternatif olarak **getClass()** ve **isInstance()** metotları kullanılabilir. Bu metotlar dinamik çalışır.

### getClass() Örneği

```java
package polymorphism;

public class A{ }

public class B{ }

public class D extends B{ }

public class Comparison{
    public static void main(String[] args) {

        System.out.println("---- Özel Sınıflar ----");
        A a1 = new A();
        B b1 = new B();
        D d1 = new D();

        System.out.println(d1.getClass().equals(A.class));
        System.out.println(a1.getClass().equals(A.class));
        System.out.println(d1.getClass().equals(B.class));

        System.out.println(a1.getClass()); // Output: class paketadı.sınıfadı
        System.out.println(b1.getClass());
        System.out.println(d1.getClass());

        System.out.println("\n---- Wrapper Sınıflar ----");

        String word = "OpenJDK";
        Integer number = new Integer(17);
        System.out.println(number.getClass().equals(Integer.class));
        System.out.println(word.getClass().equals(Integer.class));
    }
}
```

Output:

```
---- Özel Sınıflar ----
false
true
false
class polymorphism.A
class polymorphism.B
class polymorphism.D

---- Wrapper Sınıflar ----
true
false
```
<br>

 ### isInstance() Örneği
 
```java
public class Comparison {

    public static boolean fun(Object obj, String pkgAndClass)
            throws ClassNotFoundException {

        return Class.forName(pkgAndClass).isInstance(obj);
    }

    public static void main(String[] args)
            throws ClassNotFoundException {

        Integer i = new Integer(19);

        boolean b = fun(i, "java.lang.Integer");
        boolean b1 = fun(i, "java.lang.String");

        // Integer extends Number olduğu için true döndü
        boolean b2 = fun(i, "java.lang.Number");

        System.out.println(b);
        System.out.println(b1);
        System.out.println(b2);
    }
}
```

Output:

```
true
false
true
```

**Polimorfizm** ile nesne üzerinde karşılaştırma yapmadan nesnenin referansına göre işlem yapabildiğimiz için instanceof operatörünü, çalışma zamanında içinde override edilen metotların bulunduğu sınıflar ile üst sınıfı kıyaslamak amacıyla kullanmaya gerek yoktur ancak interface'lerin kullanıldığı farklı senaryolarda yer alabilirler.

```java
public interface Computer {
    void showTemperature();
}
```

```java
public class Processor implements Computer {

    @Override
    public void showTemperature() {
        System.out.println("CPU sıcaklık değeri: 65,00 Celsius");
    }

    public void showCoreUsage() {
        String usage = "CPU1: 8,7% CPU2: 2,0% CPU3: 3,0% CPU4: 4,0%\n" +
                "CPU5: 3,0% CPU6: 0,0% CPU7: 5,9% CPU8: 1,0%";

        System.out.println("İşlemci Anlık Kullanım Değerleri: \n" + usage + "\n");
    }
}
```
```java
public class GPU implements Computer {
    @Override
    public void showTemperature() {
        System.out.println("GPU sıcaklık değeri: 76,00 Celsius");
    }

    public void showInfo() {
        System.out.println("Grafik: NVIDIA® GeForce® GTX 1650");
    }
}
```

```java
public class Driver {
    public static void invoke(Computer pc) {

        pc.showTemperature();

        if (pc instanceof Processor) {
            Processor cpu = (Processor) pc; // downcasting
            cpu.showCoreUsage();
        }
        if (pc instanceof GPU) {
            GPU graph = (GPU) pc;
            graph.showInfo();
        }
    }

    public static void main(String[] args) {

        Computer pc1 = new Processor();
        Computer pc2 = new GPU();

        invoke(pc1);
        invoke(pc2);
    }
}
```

Output:

```
CPU sıcaklık değeri: 45,00 Celsius
İşlemci Anlık Kullanım Değerleri: 
CPU1: 8,7% CPU2: 2,0% CPU3: 3,0% CPU4: 4,0%
CPU5: 3,0% CPU6: 5,0% CPU7: 5,9% CPU8: 1,0%

GPU sıcaklık değeri: 56,00 Celsius
Grafik: NVIDIA® GeForce® GTX 1650
```


## Compile Time Polymorphism (Erken Bağlama)

Static Binding olarak da bilinen Polimorfizm'de nesne tipi derleme zamanında belirlenir. Java, çağıracağı metodu imzasına bakarak bilir. Compile time polimorfizm, metot **overloading** yapılarak elde edilir. Overloading'de aynı isimde birden fazla fonksiyon yazılabilir ancak bu metotların **parametre sırası**, **tipi** ve **sayısından** en az biri farklı olmalıdır. Meotodun **dönüş tipi** overloding için önemli değildir.

Örnek overloding yapısı,

```java
void func() { ... }
void func(int a) { ... }
float func(double a) { ... }
float func(int a, float b) { ... }
```
Burada metotlar aldıkları parametrelere göre farklı işlemler gerçekleştirecektir.

**``Not:``** Üst sınıf metodunun alt sınıflarda override edilerek runtime polimorfizm'in gerçekleştirilmesini istemiyorsak, bu metodu ``private``, ``final`` veya ``static`` olarak tanımlamamız gerekir. 

```java
public class Parent {

    public static final void display(char symbol) { // compile time polimorfizm
        for (int i = 0; i < 10; i++) {
            System.out.print(symbol);
        }
    }
}
```

```java
public class Child extends Parent {

    public void display(char symbol, int x, int y) { // compile time polimorfizm
        for (int i = 0; i < y; i++) {
            for (int j = 0; j < x; j++) {
                if (i == 0 || i == y - 1)
                    System.out.print(symbol);
                else {
                    if (j == 0 || j == x - 1)
                        System.out.print(symbol);
                    else
                        System.out.print(" ");
                }
            }
            System.out.println(" ");
        }
    }

    public void display() { // overloading
        System.out.println("\nInfo: 'display(char)' cannot override 'display(char)' " +
                "in 'polymorphism.Parent'; overridden method is final\n");
    }

   /* public static final void display(char symbol) { override edilemedi

     ...

    }*/
}
```

```java
public class Driver {
    public static void main(String[] args) {

        Child d1 = new Child();
        d1.display('a', 10, 4);
        d1.display();

        Parent.display('*');
    }
}
```

Output:

```
aaaaaaaaaa 
a        a 
a        a 
aaaaaaaaaa 

Info: 'display(char)' cannot override 'display(char)' in 'polymorphism.Parent'; overridden method is final

**********
```

### Operator Overloading

Java'da bazı operatörler farklı operantlarla farklı işlemler gerçekleştirir. Örneğin,

- ``+`` operatörü hem sayısal ifadeleri toplama (integers ve floating-point numbers) hem de String ifadeleri birbirine sıralı şekilde birleştirme işlemini gerçekleştirebilmesi için overload edilmiştir.
- `&`, `|` ve `!` gibi operatörler de bitsel ve mantıksal işlemleri gerçekleştirebilmesi için overload edilmiştir.

Operatör overloading ile nasıl polimorfizm yapıldığını inceleyelim.

```java
int a = 5;
int b = 6;

// + with numbers
int sum = a + b;  // Output = 11
```

```java
String first = "Java ";
String second = "Programming";

// + with strings
name = first + second;  // Output = Java Programming
```
Burda **``+``** operatörü overload edilerek **toplama** (addition) ve **birleştirme** (concatenation) işlemini gerçekleştirdi.

**``Not:``** C++ gibi dillerde operatör, farklı operantlarla farklı çalışacak şekilde tanımlanabiliyorken; Java kullanıcı tanımlı (user-defined) operatörle overloding işlemini desteklemez.


| **``Compile Time Polymorphism``** | **``Runtime Polymorphism``** |
|------|------|
| Compile time polimorfizmde, çağrılar derleyici tarafından çözülür.|  Runtime polimorfizmde, çağrılar JVM tarafından çözülür. |
| Static binding, early binding ve overloading olarak da bilinir. | Dynamic binding, late binding ve overriding olarak da bilinir. |
| Metot overloading, farklı parametre veya imzalarla aynı ismi paylaşan birden çok metodun derleme anı polimorfizmidir. | Metot overriding, aynı parametre veya imazlara sahip farklı sınıflarla ilişkili aynı isimdeki metotların runtime polimofizmidir. |
| Çalıştırılacak metodun derleme anında belli olması sayesinde bu polimorfizm çalışma anına göre daha hızlı yürütülür. | Çalıştırılacak metodun çalışma anında belirlenmesi nedeniyle erken bağlamaya göre daha yavaş yürütülür. |
| Compile time polimorfizmde, her şey derleme anında yürütüldüğü için daha az esnektir. | Run time polimorfizmde, her şey çalışma zamanında yürütüldüğü için daha esnektir. |






