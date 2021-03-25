
# Nested Classes (İç İçe Sınıflar)

<p align="center">
<img 
src="https://github.com/barisdalyan/trash/blob/master/nested_classes.png" alt="@barisdalyan" height="250" width="425" />
</p>

Java dilinde çoklu kalıtım yoktur. Java çoklu kalıtımı **interface** (arayüz) ve **iç içe sınıflar** ile sağlar. İç içe sınıflar, sınıf içinde tanımlanmış sınıflar şeklinde ifade edilebilir. İç içe sınıflar, geliştiriciye sınıflar arasında mantıksal gruplamalar yapmasına yardımcı olur. Bu durum, **encapsulation** kullanımını arttırır ve daha okunabilir, sürdürülebilir kodların yazılmasını sağlar.

Nested sınıflar iki ana gruba ayrılır:
- Static Nested  Sınıflar 
- Non-Static Nested Sınıflar (Dahili Sınıflar)

## Non-Static Nested Class (Inner Class) 
***static*** olmayan nested sınıf, sınıf içinde tanımlı bir sınıftır. Bu sınıf,  kapsayıcı sınıfının (outer class) birer üyesi konumundadır ve erişim belirleyicisi **public**, **protected**, **private** veya **package private (default)** olabilir. Dahili sınıflar, kendisini kaplayan sınıfın alanlarına ve metotlarına (**private** belirteciyle tanımlı olanlar da dahil) doğrudan erişime hakkına sahiptir. Bu özellik kapsayıcı sınıf ve aynı kapsayıcı sınıf içinde tanımlı inner sınıflar için de geçerlidir. Yani kapsayıcı sınıf metotları, dahili sınıfların nesneleri aracılığıyla bu sınıfların her türlü elemanlarına ve metotlarına **erişebilir.** Aynı şekilde, inner sınıflar da metotları içinde diğer inner sınıfları örnekleyerek bu sınıfların alan ve metotlarına ulaşabilir. Inner sınıflar, outer sınıfa bağlı olduğu için önce outer sınıfı oluşturulur, daha sonra bu sınıfın referansı ile inner sınıf oluşturulur. 

Kapsayıcı sınıf ile dahili sınıflar veya dahili sınıflar arasındaki erişimlerde, erişim belirteçleri **önemsizdir** ancak başka bir sınıftan, outer sınıf aracılığıyla dahili sınıflara ve bu sınıfların alan/metotlarına ulaşılmaya çalışıldığında erişim belirteçleri normal sınıflarda olduğu gibi erişimi kısıtlamak amacıyla kullanılabilir.

```java
public class Computer {  
    public class Motherboard {  
        // 1.dahili üye sınıf  
  
        private int memorySlots = 2;  
  
        public void getProcessorData() {  
            Processor processor = new Processor();  
            processor.start();  
            System.out.println(processor.info);  
        }  
    }  
  
    private class Processor {  
        // 2.dahili üye sınıf  
  
        private String info = "Microprocessor: Intel® Core™ i7 9750H\n" +  
                "Cache: 12 MB\n" +  
                "Number of Cores: 6";  
  
        private void start() {  
            System.out.println("> Processor is being started.");  
        }  
    }  
  
    public class RAM {  
        // 3.dahili üye sınıf  
  }  
}
```


```java
public class Driver {  
    public static void main(String[] args) {  
  
        Computer.Motherboard board = new Computer().new Motherboard();  
        board.getProcessorData();  
        System.out.println(board.memorySlots);  
        // 'memorySlots' has private access in 'Computer.Motherboard': derleme hatası  
  
	/* ya da önce Computer örneğini oluşturur, sonrasında bu nesne ile dahili sınıfı yaratırız  
	Computer pc = new Computer(); Computer.Motherboard board = pc.new Motherboard(); */  
	
        Computer.Processor processor = new Computer().new Processor();  
        // 'Computer.Processor' has private access in 'Computer': derleme hatası  
  
  }  
}
```

Output:
```
> Processor is being started.
Microprocessor: Intel® Core™ i7 9750H
Cache: 12 MB
Number of Cores: 6
```


### Dahili  Sınıflar ve Erişim Belirteçleri

Inner sınıflar outer sınıfın birer üyesi olduğu için erişim belirteçlerinin **`private`** olması durumunda, başka bir sınıftan kapsayıcı (enclosing) sınıf aracılığıyla çağırılamaz. Aşağıdaki örnekte kapsayıcı sınıf *InnerClassExample*, private inner sınıf ise *FibonacciSeries*'dır. Eğer **main** metodu kapsayıcı sınıf içinde tanımlanmasaydı inner sınıfa ulaşılamazdı.


```java
import java.util.ArrayList;

public class InnerClassExample {

    public class PrimeNumber {
        // 1.dahili sınıf asal sayı hesaplama için kullanılır
        public boolean isPrimerNumber(int number) {
            boolean control = true;

            for (int i = 2; i < number; i++) {
		if (number % i == 0) {  
		    control = false;  
		    break;  
		}
            }
            return control;
        }
    }

    // 2.dahili sınıf mükemmel sayı hesaplama için kullanılır
    protected class PerfectNumber {
        // kendisi hariç böleneleri toplamı kendisine eşit olan sayı mükemmel sayıdır.
        protected boolean isPerfectNumber(int number) {
            int sumOfDivisor = 0;
            boolean control = false;

            for (int i = 1; i < number; i++) {
                if (number % i == 0)
                    sumOfDivisor += i;
            }
            if (number == sumOfDivisor) {
                control = true;
                return control;
            } else
                return control;
        }
    }

    // 3.dahili sınıf fibonacci serisi elemanlarını bulmak için kullanılır
    private class FibonacciSeries {
        // fibonacci dizisi, her sayının kendinden öncekiyle toplanması
        // sonucu oluşan sayı dizisidir. İlk iki elemanı 1'dir.

        private ArrayList findSeries(int elementNumber) {
            ArrayList<Integer> fibonacciList = new ArrayList<>();
            fibonacciList.add(0, 1);
            fibonacciList.add(1, 1);

            for (int i = 0; i < elementNumber - 2; i++)
                fibonacciList.add(i + 2, fibonacciList.get(i)
                        + fibonacciList.get(i + 1));

            return fibonacciList;
        }
    }

    // InnerClassExample sınıfına ait main metodu
    public static void main(String[] args) {

        InnerClassExample outer = new InnerClassExample();
        PrimeNumber prime = outer.new PrimeNumber();
        System.out.println(prime.isPrimerNumber(13));

        PerfectNumber perfect = outer.new PerfectNumber();
        System.out.println(perfect.isPerfectNumber(18));

        FibonacciSeries fibonacci = outer.new FibonacciSeries(); // derleme hatası alınmadı
        System.out.println(fibonacci.findSeries(7));
    }
}
```

Output:

```
true
false
[1, 1, 2, 3, 5, 8, 13]
```

*main* veya içinde çağrıldığı metot başka bir sınıfta tanımlanması halinde: 

```java
public class Driver{
    public static void main(String[] args) {
        
        InnerClassExample outer = new InnerClassExample();
        InnerClassExample.PrimeNumber prime = outer.new PrimeNumber();
        System.out.println(prime.isPrimerNumber(13));

        InnerClassExample.PerfectNumber perfect = outer.new PerfectNumber();
        System.out.println(perfect.isPerfectNumber(18));

        // InnerClassExample.FibonacciSeries fibonacci = outer.new FibonacciSeries(); derleme hatası oluşur
        // System.out.println(fibonacci.findSeries(7));
    }
}
```

<br>

Bu örnekte bir inner sınıfın outer sınıfı elemanlarına nasıl eriştiği incelenmiştir. Daha öncede bahsedildiği gibi bir inner sınıfın, kapsayıcısının private elemanlarına erişmesi mümkündür. Burada `OuterClass.this.fields/method` şeklinde bir hiyerarşi kullanılmasının sebebi isim çakışmasının önüne geçmektir. *int name* gibi bir değişkenin olması halinde program `Java - 0` çıktısı verir.


```java
 public class Outer {
    private String name = "OpenJDK";
    private int version = 11;

    public class InnerMember {
        // int name; 
        public void print() {
            if (Outer.this.name.equals("OpenJDK")) {
                System.out.println("Java - " + name);
                System.out.println("Current version: " + version);
            }else {
                // ...
            }
        }

        public void multiply(int a, int b) {
            System.out.println("Latest version: " + a * b);
        }
    }
}
```

```java
public class Driver {
    public static void main(String[] args) {

        Outer outer = new Outer();
        Outer.InnerMember member = outer.new InnerMember();
        member.print();
        member.multiply(5, 3);
    }
}
```


Output:
```
Java - OpenJDK
Current version: 11
Latest version: 15
```

## Static Nested Class

Java'da bir sınıf içine **`static`** sınıflar da tanımlayabiliriz. Static nested sınıflar kapsayıcısını static bir üyesidir. Kapsayıcı sınıf, static nested sınıfın tüm alan ve metotlarına ulaşabilir. Static nested sınıflara ulaşmak için kapsayıcı sınıfın bir örneğine ihtiyaç yoktur.

**`Not:`** Inner ve static nested sınıfların **yapıcı metotları** bulunabilir. Java'da sadece nested sınıfların `static` tanımlanmasına izin verilmiştir. 

```java
public class NestedClassExample {
    public class InnerMember {
        private int x;
        private int y;

        public InnerMember(int a, int b) { // constructor
            x = a;
            y = b;
        }

        public void multiply() {
            System.out.println("Çarpma sonucu: " + (x * y));
        }
    }

    // static nested sınıf ve metotları
    public static class StaticMember {

        public static void addition(int a, int b) {
            System.out.println("Toplama sonucu: " + (a + b));
        }

        public void subtraction(int a, int b) {
            System.out.println("Çıkarma sonucu: " + (a - b));
        }

    }

    // NestedClassExample sınıfına ait main metodu
    public static void main(String[] args) {

        InnerMember member = new NestedClassExample().new InnerMember(6, 4);
        member.multiply();

        StaticMember.addition(5, 7);

        /* main metodu başka bir sınıfta çalıştırılırsa static metot bu şekilde çağrılırdı
        NestedClassExample.StaticMember.addition(5, 7); */

        // static sınıfın static olmayan metodunu çağırmak için bu yöntem kullanılır
        StaticMember staticMember = new StaticMember();
        staticMember.subtraction(13, 5);

        /* main veya içinde çağrıldığı metot başka bir sınıfta ise:
        NestedClassExample.StaticMember staticMember = new NestedClassExample.StaticMember(); */
    }
}
```

Output:

```
Çarpma sonucu: 24
Toplama sonucu: 12
Çıkarma sonucu: 8
```

<br>

Static nested sınıflar içinde static olan ve olmayan her türlü metot ve değişken tanımlanabilir ancak static metotlara benzer şekilde, içinde bulunduğu sınıfın static olmayan elemanlarına **erişemez.** Bunu yanında static olmayan nested sınıflara (inner sınıf) da erişemez. Bu metot ve değişkenler veya sınıflar `static` tanımlanırsa, erişim belirteçleri ne olursa olsun static nested sınıflar için erişilebilir duruma gelir. 

Inner sınıflarda (non-static nested classes) ise içinde static değişken ve metot **tanımlanamazken**, kapsayıcı sınıfının static olan ve olmayan tüm alan/metotlarına erişebilir. Buna static nested sınıflar da dahildir.

**`Not:`** Inner sınıfların içinde main() (static) metodu tanımlanamadığı için bu sınıflar komut satırından direkt olarak çalıştırılamaz ancak static nested sınıflarda bunu yapmak mümkündür.

```java
public class NestedClassExample {
    public int x = 5;
    public static final int y = 5;
    public static String name = "Mike";

    public NestedClassExample() {
        // yapıcı metot
    }

    public static void method() {
        // metot gövdesi
    }

    public void nonStaticMethod() {  
       // static olmayan metot gövdesi  
    }

    public class InnerMember {
        public int x = 7;
        private static final int y = 7; 
        public static String name = "David"; // tanımlanamaz

        public InnerMember() {
            // yapıcı metot
        }

        public static void method() { // tanımlanamaz
            // metot gövdesi
        }
        
        public void nonStaticMethod() {  
           // static olmayan metot gövdesi  
        }
    }

    public static class StaticMember {
        public int x = 13;
        public static final int y = 13;
        public static String name = "Dean";

        public StaticMember() {
            // yapıcı metot
        }

        public static void method() {
            // metot gövdesi
        }
        
        public void nonStaticMethod() {  
            // static olmayan metot gövdesi  
        }
    }
}
```

Yukarıdaki örnekte InnerMember sınıfı içindeki `private static final int y = 7` değişkeni **sabit** (constant) olduğu bu sınıfta tanımlanabildi.  **private** olmasına rağmen StaticMember sınıfı ve NestedClassExample (kapsayıcı sınıf),  bu değişkene metotları aracılığıyla **`InnerMember.y`** şeklinde ulaşabilir ancak farklı bir sınıftan bu değere ulaşılamazdı.

<br>

**`Not:`** Bir sınıf içinde nested sınıf tanımlayabiliyorduk. Bu nested sınıf içinde de **yine bir nested sınıf** tanımlayabiliriz.

```java
public class NestedClassExample {  
    public static class StaticMember1 {  
        public static class StaticMember2 {  
            public static void print() {  
                System.out.println("En içteki static sınıfın metodu çalıştı");  
            }  
        }  
    }  
  
    public static void main(String[] args) {  
        StaticMember1.StaticMember2.print();  
  
        /* print() metodu static olmasaydı:  
	 StaticMember1.StaticMember2 obj = new StaticMember1.StaticMember2(); */  
 }  
}
```

Output:

```
En içteki dahili sınıfın metodu çalıştı
```
Başka bir sınıf içinde kullanacağımız sınıfı **`import`** etmek kodun okunurluğunu arttırır.  

```java
import innerclass.NestedClassExample.StaticMember1.StaticMember2;
```

```java
public class Driver {
    public static void main(String[] args) {
        StaticMember2.print();
    }
}
```


#### Key Points

- Java inner sınıflara (non-static nested classes) normal sınıf elemanlarıymış gibi davranır. Bu sınıflar, sınıf içinde tanımlı nesne değişkenleri ve mototlar gibidir.
- Nested sınıflar, outer sınıfların üyeleri olduğu için `private`, `protected` gibi erişim belirteçleriyle (access modifiers) tanımlanabilir ancak bu durum outer sınıflar için geçerli değildir.
- Inner sınıf nesnesi outer sınıf nesnesinden bağımsız var olamazken, static-nested sınıflar outer sınıf nesnesinden bağımsız olabilir ancak her iki nested sınıfın da sınırı (scope) kapsayıcısına bağlıdır.
- Non-static nested sınıflar, outer/enclosing sınıfların private üyelerine erişebilirken, static nested sınıflar `static` tanımlı private değişken ve metotlara erişebilir.

<br>

### Inner Interfaces

Bir **sınıf** veya **interface** içinde tanımlanan arayüzlere inner interface denir. Temel amacı ilgili interface veya sınıfla arasında bir ilişkisi bulunan interface'leri gruplamaktır. Bu tür arayüzler kapsayıcı sınıf veya arayüz aracılığıyla kullanılır.

**Örnek:** Map interface'i içindeki Entry interface'i, bir nested arayüzdür. Böylece Map.Entry ile bu interface'e ulaşabiliriz.

- Nested interface'ler default olarak **static** tanımlıdır.
- Sınıf içinde tanımlı interface'ler erişim belirteçleri ile kısıtlanabilirken, interface içinde tanımlı olan interface **public** tanımlıdır.

Bu son özelliğin örneğini interface konusunda yapmıştık ancak tekrar olması bakımından bir örnek daha yapalım.


```java
public interface MyInterfaceA{
    void display();
    interface MyInterfaceB{
        void method();
    }
}
```

```java
public class NestedInterfaceExample implements MyInterfaceA.MyInterfaceB{

    @Override
    public void method() {
        System.out.println("Nested interface metodu çalıştı");
    }

    public static void main(String[] args) {
        MyInterfaceA.MyInterfaceB obj = new NestedInterfaceExample();
        obj.method();
    }
}
```

Output:

```
Nested interface metodu çalıştı
```

<br>

Sınıf içinde tanımlı nested interface örneği:

```java
public class MyClass {
    protected interface MyInterfaceB {
        void method();
    }
}
```

```java
public class NestedInterfaceExample implements MyClass.MyInterfaceB {

    @Override
    public void method() {
        System.out.println("Sınıf içinde tanımlı nested interface metodu çalıştı");
    }

    public static void main(String[] args) {
        MyClass.MyInterfaceB obj = new NestedInterfaceExample();
        obj.method();

        /* ya da
        NestedInterfaceExample newObj = new NestedInterfaceExample();
        newObj.method();*/
    }
}
```

Output:

```
Sınıf içinde tanımlı nested interface metodu çalıştı
```

### Local Inner Class (Yerel Sınıf)

Yerel sınıf, bir **blok** içinde tanımlanan dahili bir sınıftır. Genel olarak bu blok, bir metodun gövde (body) kısmı olmasının yanında döngü (loop), initialization blok ([bkz.](https://stackoverflow.com/questions/3987428/what-is-an-initialization-block)),  constructor veya koşul (if clause) ifadelerinin blokları da olabilir. Yerel sınıflar outer sınıfların bir üyesi değildir. Tanımlandıkları bloğa bağlı oldukları için erişim belirteci **default/frinedly**'dir. Bununla birlikte **final** veya **abstract** olarak da tanımlanabilirler. 

**`Not:`** Yerel sınıflar kapsayıcı sınıfa bağlı olmadığı için **static** olarak tanımlanamaz. Derleme hatası oluşur.

Local sınıflar bulunduğu bloğun sadece `final` ya da `effectively final` olarak işaretlenmiş değişkenlerine ulaşabilirken, kapsayıcı sınıfın tüm üyelerine ulaşabilir (**private** tanımlı olanlar dahil) ve sadece tanımlandığı **blok içinde** örneklenir (instantiating). Bunun dışında local sınıflar `abstract ve normal` sınıfları **extend**, `interface`'leri de **implemente** edebilir.

**`effectively final:`** Java 8 sürümüyle gelen bir terimdir. final olarak tanımlanmayan ancak bir kez değer atadıktan sonra değiştirilmeyen değişkenlerdir.

* **Yerel değişkenler ve parametreler neden final ya da effectively final olmak zorunda?**

Java'da yerel değişkenler belleğin **stack** kısmında tutulur ve içinde bulundukları metodun işi bittiğinde, bu değişkenler bellekten silinir. Bunun yanında, metot sonlansa bile yerel sınıf nesnesi belleğin **heap** kısmında var olmaya devam edebilir. Yerel sınıftan final olarak tanımlanan değişkene erişilmeye çalışıldığında JVM yerel sınıf içinde **synthetic field** (source code'da görünmez) oluşturur ve bu değişkeni heap alanına kopyalar. Böylece metot sonlansa bile yerel sınıf belleğin heap kısmından bu değişkene ulaşabilir.

* **Derleme zamanında ne olur?**

Yerel bir sınıf içeren bir program derlendiğinde, derleyici outer sınıf için ve kapsayıcı sınıfa referansı olan yerel sınıf için .class dosyası oluşturur. Bu dosyalar derleyici tarafından `Outer.class`, `Outer$1Inner.class` şeklinde isimlendirilir. Bu nedenle Java'da sınıf, metot ve alanlarda isimlendirme yaparken `$` sembolünün kullanılması önerilemez.

#### Metot Gövdesinde Tanımlama

**Örnek 1:**

```java
public interface Fonctions {
    double calculateFactorial(int number);
}
```

```java
public class LocalInnerClassExample {

    public double factorial(int number) {
        double methodResult;

        class Calculation implements Fonctions {
            private double classMethodResult = 1;

            public Calculation() { // local sınıfların constructor'ı olabilir
                System.out.println("Burası yerel sınıfın yapıcı metodu");
            }

            @Override
            public double calculateFactorial(int number) {
                for (int i = 2; i <= number; i++)
                    classMethodResult *= i;

                return classMethodResult;
            }
        }

        // yerel sınıfın nesnensi oluşturuldu
        Calculation innerClass = new Calculation();
        methodResult = innerClass.calculateFactorial(number);

        return methodResult;
    }
}
```

```java
public class Driver {
    public static void main(String[] args) {

        LocalInnerClassExample obj = new LocalInnerClassExample();
        System.out.println("7'nin faktöriyeli: " + obj.factorial(7));
    }
}
```

Output:

```
Burası yerel sınıfın yapıcı metodu
7'nin faktöriyeli: 5040.0
```

<br>

**Örnek 2:**

Yerel sınıflar kendisini kapsayan bloğun sadece **effectively final** yerel değişkenlerine ve parametrelerine erişebildiği için *float sum* değişkenine sonradan atama yaptığımızda bu değişken, effectively final özelliğini kaybeder ve ilgili derleyici hatası oluşur.

```java
public class Outer {
    private String resultText = "Quotient: ";

    public void getValue(float divisor) {
        float sum = 25;

        class Inner {

            public Inner() {
                // sum = 35; variable 'sum' is accessed from within inner class,
                // needs to be final or effectively final
                System.out.println(Outer.this.resultText + getQuotient());
            }

            private float getQuotient() {
                return sum / divisor;
            }
        }
        
        Inner inner = new Inner();
    }
}
```

```java
public class Driver {
    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.getValue(2);
    }
}
```

Output:

```
Quotient: 12.5
```

<br>

#### if Koşulu İçinde Tanımlama


```java
public class Outer {
    private int data = 13;

    public int getData() {
        return data;
    }

    public static void main(String[] args) {
        Outer outer = new Outer();

        if (outer.getData() < 17) {
            // if koşulu içinde yerel sınıf
            class Inner {

                public Inner(){
                    // constructor
                }
                public int getValue() {
                    System.out.println("Inside Inner class");
                    return outer.data;
                }
            }

            Inner inner = new Inner();
            System.out.println("Value: " + inner.getValue());
        } else
            System.out.println("Inside Outer class");
    }
}

```

Output:

```
Inside Inner class
Value: 13
```

### Anonymous Inner Class (Anonim Sınıf)

Adı olmayan ve kendisi için sadece tek bir nesnenin yaratıldığı bir dahili sınıftır. Bu sınıfların tanımlanması ve örneklenmesi aynı anda olmaktadır. Anonim sınıflar isminin olmaması dışında, genel olarak yerel sınıflara benzerdir. Sadece bir kez kullanmak istediğimizde, yerel sınıflar yerine anonim sınıflar tercih edilebilir. Böylece daha az kod yazmış oluruz. Bir isme sahip olmadıkları için yapıcı metotları yoktur. Anonim sınıflar, belirli bir amaç için bir nesnenin örneğini oluştururken kullanışlı olabilir. Gerçek bir alt sınıf oluşturmadan interface veya sınıf metotlarını override etmek mümkündür. 

Anonim dahili sınıflar genelde iki şekilde oluşturulur:
* Class (somut veya abstract)
* Interface

Anonim dahili sınıf tanımı constructor çağırmaya benzer ancak burada farklı olan, blok içinde bir sınıf tanımının olmasıdır.
   
 ```java
 // interface, abstract/concrete sınıf olabilir
    AnonymousType obj = new AnonymousType() {
        public void method() {
            // ...
        }
    };
```

Daha iyi anlaşılması için birkaç örnek yapalım.

**Örnek 1:**

```java
public interface Identity {
    void getInfo(int number, String name);
}
```

```java
public class Customer implements Identity {
    @Override
    public void getInfo(int number, String name) {
        System.out.println("ID: " + number);
        System.out.println("Customer Name: " + name);
    }
}
```

```java
public class AnonymousDemo {
    public static void main(String[] args) {

        Customer obj = new Customer();
        obj.getInfo(257, "Castiel");
    }
}
```

Output:
```
ID: 257
Customer Name: Castiel
```

Yukarıdaki örnekte, `Identity` arayüzü tanımlandı ve `Customer` bu arayüzü uyguluyor ancak ayrı bir sınıf yazmak yerine, override edilecek metot anonim sınıfta tanımlanabilirdi.

**Örnek 1'in anonim sınıfa göre uyarlanmış hali:**


```java
public interface Identity {
    void getInfo(int number, String name);
}

public class AnonymousDemo {
    public static void main(String[] args) {

        Identity obj = new Identity() {
            @Override
            public void getInfo(int number, String name) {
                System.out.println("ID: " + number);
                System.out.println("Customer Name: " + name);
            }
        };
        
        obj.getInfo(257,"Castiel");
    }
}
```
Burada Identity nesnesi oluşturulmadı çünkü interface'lerden nesne oluşturulamaz. Bunun yerine derleyici; **Identity** arayüzünü uygulayıp (implements), **getInfo()** metodunu da override eden ``AnonymousDemo$1`` adında bir sınıf üretti.  Üretilen anonim sınıf nesnesi, Identity türündeki referans değişkenini işaret eder. Yani aslında bu yapı arka planda ilk örnekteki yapıya benzer bir hal alır.
```
Derleme Sonucu: 
'AnonymousDemo$1.class'   AnonymousDemo.class   Identity.class
```
<br>

**Örnek 2:**

```java
public interface Factorial {
    double calculateFactorial();
}
```

```java
public class AnonymousInnerClassExample {

    public Factorial factorial(final int number) { 
    // number effectively final olarak da kullanılabilirdi

        return new Factorial() {

            @Override
            public double calculateFactorial() {
                double methodResult = 1;

                for (int i = 2; i <= number; i++)
                    methodResult *= i;

                return methodResult;
            }
        };
    }
}
```

```java
public class Driver {
    public static void main(String[] args) {

        AnonymousInnerClassExample obj = new AnonymousInnerClassExample();
        Factorial f = obj.factorial(8);
        System.out.println("8'in faktöriyeli: " + f.calculateFactorial());
    }
}
```

Output:

```
8'in faktöriyeli: 40320.0
```

Anonim sınıflar, kapsayıcı bloğun `final` veya `effectively final` olmayan yerel değişken ve parametrelerine **erişemez.** Bunun sebebini yerel dahili sınıflarda açıklamıştık.



**Anonim dahili sınıfların türleri:** Tanımlandığı yere ve davranışına göre üç tür anonim sınıf vardır.

1. **Bir sınıfı extend eden Anonim Inner Sınıf:** Anonim sınıflar, bir sınıfı genişletmek için kullanılabilir. Örneğin, bir thread oluşturmak için `Thread` sınıfını miras almak yerine anonim sınıflarla kullanıma hazır thread oluşturabiliriz.


```java
public class MyThread {
    public static void main(String[] args) {

        Thread newThread = new Thread() {
            public void run() {
                System.out.println("Alt Thread çalıştı");
            }
        };
        newThread.start();
        System.out.println("Ana Thread çalıştı");
    }
}
```
Output:

```
Ana Thread çalıştı
Alt Thread çalıştı
// Ya da
Alt Thread çalıştı
Ana Thread çalıştı
```

2. **Bir arayüzü implemente eden Anonim Inner Sınıf:** Anonim sınıflar, bir interface'i uygulamak için de kullanılabilir. Örneğin, `Runable` arayüzünü implemente ederek de bir thread oluşturabiliriz. Burada anonim sınıf arayüzü uygulayarak thread oluşturur.

```java
public class MyThread {
    public static void main(String[] args) {

        Runnable runnable = new Runnable() {
            public void run() {
                System.out.println("Alt Thread çalıştı");
            }
        };
        
        Thread newThread = new Thread(runnable);
        newThread.start();
        System.out.println("Ana Thread çalıştı");
    }
}
```
Output:

```
Ana Thread çalıştı
Alt Thread çalıştı
// Ya da
Alt Thread çalıştı
Ana Thread çalıştı
```

3. **Bir metot/constructor içinde argüman olarak tanımlı Anonim Inner Sınıf:** Anonim sınıflar, bir metot/constructor argümanı olarak tanımlanabilirler. Bu tür tanımlamalar grafiksel kullanıcı arayüzü (GUI) programlarken kullanılır. Java'da Swing ile uğraşanlar bilir, program aşağıdaki gibi bir yapıdan başlar. Burada metoda parametre olarak  `Runnable` arayüzü geçilmiş ve bu arayüzden anonim sınıf oluşturularak `run()` metodu overrride edilmiş.

**Örnek 1:**

```java
      /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() { // It listens the events and orders them in thread.
            @Override
            public void run() {
                new Dictionary().setVisible(true);
            }
        });
```

**Örnek 2:**

```java
  public class MyThread {
    public static void main(String[] args) {

        Thread newThread = new Thread(new Runnable() {
            public void run() {
                System.out.println("Alt Thread çalıştı");
            }
        });

        newThread.start();
        System.out.println("Ana Thread çalıştı");
    }
}
```
Output:

```
Ana Thread çalıştı
Alt Thread çalıştı
// Ya da
Alt Thread çalıştı
Ana Thread çalıştı
```

**Normal sınıf ile anonim inner sınıf arasındaki farklar nelerdir?**

* Normal bir sınıf birden çok interface'i uygulayabilirken, anonim sınıf bir seferde bir interface'i uygulayabilir.
* Normal bir sınıf aynı anda bir sınıfı miras alırken, birden çok interface'i uygulayabilir ancak anonim sınıflar bir sınıfı extend veya bir interface'i implemete edebilir. Aynı anda ikisini yapamaz.
* Normal sınıfların birden çok yapıcı metodu bulunabilirken, anonim sınıfların isimleri olmadığı için constructor'ları da olmaz.

**Kapsayıcı Bloğun Yerel Değişkenlerine Erişme**

Yerel Inner sınıflar gibi anonim sınıflar da yerel değişkenleri yakalayabilir. Bu iki sınıf yerel değişkenlere aynı şekilde erişir:
* Anonim sınıflar kapsayıcı sınıfının değişkenlerine erişebilir (**private** erişim belirtecine sahip olanlar dahil).
* Daha öncede bahsettiğimiz gibi anonim sınıflar kapsayıcı bloğun `final` veya `effectively final` olmayan yerel değişken ve parametrelerine **erişemez.**
* Nested sınıflarda olduğu gibi anonim sınıf içinde tanımlı olan bir ifade (bu bir değişken olabilir) kapsayıcı sınıfı içindekiyle aynı isimde ise anonim sınıf bu tanımlamayı gölgeler (shadows). 

**Anonim Inner Sınıfların Üyelerini Tanımlama ve Erişme**

Anonim sınıflar, yerel sınıflar ile aynı kısıtlamalara sahiptir:
* Anonim sınıflar içinde static initializer ve üye interface'ler tanımlanamaz.
* Anonim sınıflar sabit olarak tanımlanması şartıyla static üyelere sahip olabilir (static final değişken).

**`Not:`** Anonim sınıflar içinde:
* Alanlar (fields), 
* Ekstra metotlar (üst türün (supertype) herhangi bir metodunu uygulamasa bile), 
* Instance initializer blok ve yerel sınıflar tanımlanabilir.
