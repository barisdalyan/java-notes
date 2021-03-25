
# Math Class

**Math** sınıfı `java.lang` paketinde yer alan, bünyesinde **matematiksel işlemler** yapmak için çeşitli metotlar barındıran bir sınıftır. Math sınıfı içindeki metotlar ve alanlar **static** tanımlandığı için bu metotlara sınıf adıyla ulaşmak mümkündür.

## Math.pow() Metodu
Bu metot üs alma işlemi yapar. İki parametre alır, ilk parametre üssü alınacak sayıdır diğer parametre ise üssün derecesidir.

```
public static double pow(double a, double b)
```

```java
public class Driver {
    public static void main(String[] args) {
        
        System.out.println(Math.pow(3, 5));
        int powVar = (int) Math.pow(2, 6); // casting
        System.out.println(powVar);
    }
}
```

Output:
```
243.0
64
```
Yukarıdaki örnekte pow() metodu **double** değer döndüğü için **powVar** değişkeninde atama yaparken casting işlemi uygulandı.

## Math.sqrt() Metodu
Bu metot bir sayının **karekökünü** bulur. Dolayısıyla bir parametre alır.

```
public static double sqrt(double a)
```

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println(Math.sqrt(25));
        int sqrtVar = (int) Math.sqrt(25);
        System.out.println(sqrtVar);
        System.out.println(Math.sqrt(37));
    }
}
```

Output:
```
5.0
5
6.082762530298219
```

## Math.abs() Metodu
Bu metot bir sayının **mutlak değerini** alır. Sayı negatif ise pozitif değere çevirdikten sonra döndürür ancak sayı pozitif ise aynen döndürür.

```
public static int abs(int a)
public static long abs(long a)
public static float abs(float a)
public static double abs(double a)
```

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println(Math.abs(-71.5));
        int varAbs = Math.abs(-71);
        System.out.println(varAbs);
        System.out.println(Math.abs(28));
    }
}
```

Output:
```
71.5
71
28
```

## Math.floor() Metodu
Bu metot verilen bir tam sayıyı **altındaki değere** yuvarlar. Bir nevi virgülden sonraki kısmı atar.

```
public static double floor(double a)
```

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println(Math.floor(3.4));
        int varFloor1 = (int) Math.floor(5.501);
        System.out.println(varFloor1);
        double varFloor2 = Math.floor(7.0001);
        System.out.println(varFloor2);
        System.out.println(Math.floor(9));
    }
}
```

Output:
```
3.0
5
7.0
9.0
```

## Math.ceil() Metodu
Bu metot **Math.floor()** metodunun aksine, sayıyı üst değere yuvarlar. Bir nevi virgülden sonraki kısmı atar ve kalan sayıyı bir arttırır.

```
public static double ceil(double a)
```

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println(Math.ceil(4.0001));
        int varCeil = (int) Math.ceil(7.9999);
        System.out.println(varCeil);
        System.out.println(Math.ceil(7));
    }
}
```

Output:
```
5.0
8
7.0
```

## Math.round() Metodu
Bu metot **ondalık** (decimal) sayıları en yakın **int** ya da **long** değerine yuvarlar.

```
public static int round(float a)
```
Özel durumlar:

- Eğer parametre NaN ise 0 döner.
- Eğer parametre negatif sonsuzluktaysa veya Integer.MIN_VALUE değerinden küçük ya da eşit herhangi bir değer ise dönen değer Integer.MIN_VALUE değerine eşit olur.
- Eğer parametre pozitif sonsuzluktaysa veya Integer.MAX_VALUE değerinden büyük ya da eşit herhangi bir değer ise dönen değer Integer.MAX_VALUE değerine eşit olur.

```
public static long round(double a)
```
Özel durumlar:

- Eğer parametre NaN ise 0 döner.
- Eğer parametre negatif sonsuzluktaysa veya Long.MIN_VALUE değerinden küçük ya da eşit herhangi bir değer ise dönen değer Long.MIN_VALUE değerine eşit olur.
- Eğer parametre pozitif sonsuzluktaysa veya Long.MAX_VALUE değerinden büyük ya da eşit herhangi bir değer ise dönen değer Long.MAX_VALUE değerine eşit olur.

**``Not:``**
```
int MIN_VALUE = -2147483648;  
int MAX_VALUE = 2147483647;

long MIN_VALUE = -9223372036854775808L;  
long MAX_VALUE = 9223372036854775807L;
```

**Örnek 1:**
```java
public class Driver {
    public static void main(String[] args) {

        float a1 = -83.76f;
        // float için en yakın int değerini bulur
        System.out.println(Math.round(a1));

        float a2 = -50.50f;
        System.out.println(Math.round(a2));

        double b1 = 79.49;
        // double için en yakın long değerini bulur
        System.out.println(Math.round(b1));

        double b2 = 50.50;
        System.out.println(Math.round(b2));
    }
}
```
Output:
```
-84
-50
79
51
```
<br>

**Örnek 2:**
```java
public class Driver {
    public static void main(String[] args) {

        float negativeInfinity = Float.NEGATIVE_INFINITY;
        // Input negative Infinity, Output Integer.MIN_VALUE
        System.out.println(Math.round(negativeInfinity));

        double positiveInfinity = 1.0 / 0;
        // Input positive Infinity, Output Long.MAX_VALUE
        System.out.println(Math.round(positiveInfinity));

        double NaN = 0.0 / 0;
        System.out.println(Math.round(NaN));
    }
}
```
Output:
```
-2147483648
9223372036854775807
0
```

## Math.max() Metodu
Bu metot parametre geçilen iki sayıdan büyük olanı döndürür.

```
public static int max(int a, int b)
public static long max(long a, long b)
public static float max(float a, float b)
public static double max(double a, double b)
```

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println(Math.max(55, 56));
        System.out.println(Math.max(7, 6.1));
        System.out.println(Math.max(4, 4.0001));
        System.out.println(Math.max(4, 5));
    }
}

```

Output:
```
56
7.0
4.0001
5
```

## Math.min() Metodu
Bu metot **Math.max()** metodunun aksine parametre geçilen iki sayıdan küçük olanı döndürür.

```
public static int min(int a, int b)
public static long min(long a, long b)
public static float min(float a, float b)
public static double min(double a, double b
```

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println(Math.min(55, 56));
        System.out.println(Math.min(7, 6.1));
        System.out.println(Math.min(4, 4.0001));
        System.out.println(Math.min(4, 5));
    }
}
```

Output:
```
55
6.1
4.0
4
```

## Math.random() Metodu
Bu metot **0.0** değerine eşit veya bu değer ile **1.0** (dahil değil) arasında, **double** tipinde bir değer döner. Döndürülen değer, bu aralıktan eşit olasılıkla (equally likely - uniform distribution) rastgele seçilir. Metot ilk kez çağırıldığında, aşağıdaki tanımlamada olduğu gibi tek bir **pseudorandom-number generator** (sözde rastgele sayı üreticisi) oluşturur.

```
new java.util.Random()
```
Bu yeni pseudorandom-number generator, metoda yapılan tüm çağrılarda kullanılır. Bunun dışında başka bir yerde kullanılmaz. 

Metot, birden fazla thread (iş parçacığı) tarafında doğru kullanılabilmesi için uygun şekilde senkronize edildi.  Böylece, birden çok thread'in büyük oranda  rastgele sayı üretmesi gerektiği durumlarda, thread'ler arasında kendi pseudorandom-number generator'larını üretmek için çıkabilecek çekişme (contention) azalır. 

**Örnek 1:**
```java
public class Driver {
    public static void main(String[] args) {

        System.out.println(Math.random()); // 0.0-1.0 arasında sayı üretecektir
        System.out.println((int) (Math.random() * 10)); // 0-10 arasında sayı üretecektir
        System.out.println((int) (Math.random() * 10 + 15)); // 0-25 arasında sayı üretecektir
    }
}
```

Output:
```
0.6649056562534362
5
18
```
Yukarıdaki örnekte **``1.0``**, **``10``** ve **``25``** değerleri rastgele seçime dahil değildir.
<br>

**Örnek 2:**
```java
public class Driver {
    public static void main(String[] args) {

        for (int i = 0; i < 4; i++) {
            int var = (int) (Math.random() * 127);
            System.out.print(var + " ");
        }
    }
}
```

Output:
```
126 50 8 89
```

## Math.toDegrees() Metodu
Bu metot **radyanı dereceye** çevirmek için kullanılır. Parametre olarak aldığı **double** değerin **derece** karşılığını döndürür.

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println("0.5 Radyan " + Math.toDegrees(0.5) + " derecedir.");
        System.out.println("1 Radyan " + Math.toDegrees(1) + " derecedir.");
        System.out.println("2.5 Radyan " + Math.toDegrees(2.5) + " derecedir.");
    }
}
```

Output:
```
0.5 Radyan 28.64788975654116 derecedir.
1 Radyan 57.29577951308232 derecedir.
2.5 Radyan 143.2394487827058 derecedir
```

## Math.toRadians() Metodu
Bu metot **toDegrees()** metodunun aksine parametre olarak aldığı **derece** cinsinden değeri **radyan** cinsine çevirir. Dönen değer **double** tipindedir.

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println("0° -> " + Math.toRadians(0) + " radyandır.");
        System.out.println("45° -> " + Math.toRadians(45) + " radyandır.");
        System.out.println("90° -> " + Math.toRadians(90) + " radyandır.");
    }
}
```

Output:
```
0° -> 0.0 radyandır.
45° -> 0.7853981633974483 radyandır.
90° -> 1.5707963267948966 radyandır.
```

## Math.sin() Metodu
Bu metot trigonometrik işlemlerde kullanılmak üzere, parametre olarak aldığı **radyan** cinsinden açının **sinüs** değerini döndürür. Dönen değer **double** tipindedir.

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println("sin(0°) = " + Math.sin(Math.toRadians(0)));
        System.out.println("sin(45°) = " + Math.sin(Math.toRadians(45)));
        System.out.println("sin(90°) = " + Math.sin(Math.toRadians(90)));
    }
}
```

Output:
```
sin(0°) = 0.0
sin(45°) = 0.7071067811865475
sin(90°) = 1.0
```

## Math.asin() Metodu
Bu metot **Math.sin()** metodun tersine parametre olarak **sinüs** değerini alır ve bu sinüs değerine karşılık gelen açıyı **radyan** cinsinden döner. Dönen değer **double** tipindedir.

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println("Derece: " + Math.toDegrees(Math.asin(0)));
        System.out.println("Derece: " + Math.toDegrees(Math.asin(0.7071067811865476)));
        System.out.println("Derece: " + Math.toDegrees(Math.asin(1)));
    }
}
```

Output:
```
Derece: 0.0
Derece: 45.00000000000001
Derece: 90.0
```

## Math.cos() Metodu
Bu metot trigonometrik işlemlerde kullanılmak üzere, parametre olarak aldığı **radyan** cinsinden açının **kosinüs** değerini döndürür. Dönen değer **double** tipindedir.

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println("cos(0°) = " + Math.cos(Math.toRadians(0)));
        System.out.println("cos(45°) = " + Math.cos(Math.toRadians(45)));
        System.out.println("cos(60°) = " + Math.cos(Math.toRadians(60)));
    }
}
```

Output:
```
cos(0°) = 1.0
cos(45°) = 0.7071067811865476
cos(60°) = 0.5000000000000001
```

## Math.acos() Metodu
Bu metot **Math.cos()** metodun tersine parametre olarak **kosinüs** değerini alır ve bu kosinüs değerine karşılık gelen açıyı **radyan** cinsinden döner. Dönen değer **double** tipindedir.

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println("Derece: " + Math.toDegrees(Math.acos(1)));
        System.out.println("Derece: " + Math.toDegrees(Math.acos(0.7071067811865476)));
        System.out.println("Derece: " + Math.toDegrees(Math.acos(0)));
    }
}
```

Output:
```
Derece: 0.0
Derece: 45.0
Derece: 90.0
```

## Math.PI ve Math.E Sabiti
Math sınıfında bu iki double değer, ``static final`` olarak tanımlanmış **sabitlerdir** (constant).

```java
public class Driver {
    public static void main(String[] args) {
        
        System.out.println("PI: " + Math.PI);
        System.out.println("E: " + Math.E);
    }
}
```

Output:
```
PI: 3.141592653589793
E: 2.718281828459045
```

## Logaritma Metodları
Math sınıfı içinde farklı tabanda değer dönen üç tane logaritma metodu bulunmaktadır. 
- ``double log(double a)``: Parametre geçilen **a** değişkeninin doğal logaritmasını (e tabanında) döner. 
- ``double log10(double a)``: Parametre geçilen **a** değişkeninin 10 tabanında logaritmasını döner.
- ``double log1p(double x)``: Parametre geçilen **x** değişkeninin 1 fazlasının doğal logaritmasını döner.

```java
public class Driver {
    public static void main(String[] args) {

        System.out.println("2.718281828459045 sayısının doğal logaritması: " + Math.log(Math.E));
        System.out.println("10 tabanında 5'in logaritmik değeri: " + Math.log10(5));
        System.out.println("(1.3 + 1)'in doğal logaritması: " + Math.log1p(1.3));
    }
}
```

Output:
```
2.718281828459045 sayısının doğal logaritması: 1.0
10 tabanında 5'in logaritmik değeri: 0.6989700043360189
(1.3 + 1)'in doğal logaritması: 0.832909122935104
```

Bu sınıf hakkında daha fazla bilgi almak için [Oracle API Doc.](https://docs.oracle.com/javase/8/docs/api/index.html?java/lang/Math.html) veya [TutorialsPoint](https://www.tutorialspoint.com/java/lang/java_lang_math.htm)'i inceleyebilirsiniz.

# Random Sınıfı
Rastgele sayı (pseudorandom number) üretebilmek için Math sınıfının yanında ``java.util`` paketinde yer alan Random sınıfı da kullanılabilir. Bu sınıf rastgele sayılar üretmek için [linear congruential formülü](https://www.geeksforgeeks.org/linear-congruence-method-for-generating-pseudo-random-numbers/?ref=rp) ile değiştirilen 48-bit'lik bir **seed** kullanır. Böylece her seferinde aynı seri üretilir. Yani, iki farklı Random nesnesine aynı seed değerini verirsek sınıf metotları aynı rastgele seriyi döner. Bunu yapmak için ``java.util.Random.setSeed(long seed)`` metodu kullanılır veya ``Random(long seed)`` constructor'a bir long değeri geçilir. Random constructor'ını boş bırakırsak, sınıf her seferinde farklı bir değer üretmek için zamanı (system nano time) baz alır. 

Java Random sınıfı thread açısından güvenlidir ancak aynı Random sınıfı örneğinin iş parçacıkları arasında eşzamanlı kullanımı çekişmelerle ve düşük performansla sonuçlanacaktır. Bunun yerine, multithreaded tasarımlarda [ThreadLocalRandom](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadLocalRandom.html) sınıfının kullanılması tavsiye edilir. ThreadLocalRandom, Random sınıfının bir alt sınıfıdır ve bahsedilen çekilmeyi önlemek için her thread'de bir Random örneği oluşturur.

Java Random sınıfı kriptografik olarak güvenli değildir. Bunun yerine güvenliğe duyarlı uygulamalarda kullanılmak üzere, kriptografik olarak güvenli bir pseudorandom sayı üreteci elde etmek için [SecureRandom](https://docs.oracle.com/javase/8/docs/api/java/security/SecureRandom.html) sınıfı kullanılabilir. 

**``Not:``** Seed, formül (linear congruential) içinde bir rastgele sayı dizisi elde etmek için kullanılan ilk değerdir.

Random sınıfı tarafından uygulanan algoritmalar, her çağrıda 32'ye kadar rastgele üretilmiş bit sağlayabilen yardımcı protected metotlar kullanır. Bu metotlar int, double, long, float vb. türden rastgele sayılar döndürür.

**Örnek 1:**
```java
import java.util.Random;

public class Driver {
    public static void main(String[] args) {

        Random r = new Random();
        System.out.println("Number: " + r.nextInt(10));
        // 0-10 arasında üretecektir

        System.out.println("Int: " + r.nextInt()); // int tipinde rastgele bir değer
        System.out.println("Long:" + r.nextLong()); // long tipinde rastgele bir değer
        System.out.println("Float: " + r.nextFloat()); // 0.0 ve 1.0 arasında float tipinde rastgele bir değer
        System.out.println("Double: " + r.nextDouble()); // 0.0 ve 1.0 arasında double tipinde rastgele bir değer
        System.out.println("Boolean: " + r.nextBoolean()); // boolean tipinde rastgele bir değer
        System.out.println("Gaussian: " + r.nextGaussian()); 
    }
}
```

Output:
```
Number: 3
Int: 654226084
Long:7240613416500943869
Float: 0.6644633
Double: 0.879507693299752
Boolean: false
Gaussian: -1.1532121082741842
```
Yukarıdaki ilk örnekte ``nextInt(int bound)`` metodu **0** ile **bound** (dahil değil) arasında bir değer dönerken, altındaki örnekte ``nextInt()`` metodu **-2147483648** ve **2147483647** arasında bir değer döner.

**``Not:``** nextGaussian() metodu, ortalaması (average) **0.0** ve standart sapması (standard deviation) **1.0** olan, **double** türünde rastgele bir Gaussian ([normal distribution](https://tr.wikipedia.org/wiki/Normal_da%C4%9F%C4%B1l%C4%B1m)) değeri döner. Bu metodun aksine diğer metotlar eşit olasılıkta değer dönerken, bu metot *olasılık yoğunluk fonksiyonuna (probability density function)* göre **ortalama** civarında/etrafında bir değer döner. Bu metot hakkında daha fazla bilgi için şu yazıları ([1](https://www.javamex.com/tutorials/random_numbers/gaussian_distribution.shtml) ve [2](https://www.javamex.com/tutorials/random_numbers/gaussian_distribution_2.shtml)) okumanızı öneririm.  

**Örnek 2:**
```java
import java.util.Random;

public class Driver {
    public static void main(String[] args) {
        
        int[] array = new int[5];
        Random random = new Random();
        for (int i = 0; i < array.length; i++) {
            array[i] = random.nextInt(100);
            System.out.println("Dizinin " + (i + 1) + ".elemanı: " + array[i]);
        }
    }
}
```

Output:
```
Dizinin 1.elemanı: 61
Dizinin 2.elemanı: 44
Dizinin 3.elemanı: 59
Dizinin 4.elemanı: 54
Dizinin 5.elemanı: 78
```
<br>

**Örnek 3:**
```java
import java.util.Random;

public class Driver {
    public static void main(String[] args) {

        Random random = new Random();

        for (int i = 0; i < 3; i++) {
            int number1 = random.nextInt(6);
            number1 += 1;
            int number2 = random.nextInt(6);
            number2 += 1;

            System.out.println("Zarda gelen sayılar: ");
            System.out.println(number1 + " - " + number2);
        }
    }
}
```

Output:
```
Zarda gelen sayılar: 
2 - 6
Zarda gelen sayılar: 
3 - 5
Zarda gelen sayılar: 
4 - 2
```

Bu sınıf hakkında daha fazla bilgi almak için [Oracle API Doc.](https://docs.oracle.com/javase/8/docs/api/index.html?java/util/Random.html) veya [TutorialsPoint](https://www.tutorialspoint.com/java/util/java_util_random.htm)'i inceleyebilirsiniz.



