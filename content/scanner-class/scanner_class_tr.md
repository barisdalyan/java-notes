
# Scanner Class

**``java.util``** paketi içindeki **Scanner** sınıfı; int, short, long, float, double vb. primitive ve String tipleri **regular expression**'larla çözümleyen bir metin tarayıcısıdır. **Input streams**, **kullanıcı** ve **dosya** gibi farklı kaynaklardan girilen verileri (input data) okumak için kullanılır. Scanner sınıfı, girdileri **token**'lara (işaret/belirteç) ayırmak için bir sınırlayıcı (delimiter) kullanır. Bu sınırlayıcı varsayılan olarak "**boşluk**" (whitespace) karakteridir.  

**``Not:``** Regular Expression'lar veya kısaca **Regex**; Java'da bir String'i aramak, manipüle etmek ve düzenlemek için kullanılan String Pattern'leri (desen)
tanımlamaya yarayan bir API'dır. Regex'ler ``java.util.regex`` paketi altında tanımlıdır. Email doğrulama ve parolalar kısıtlama tanımlamaları yapmak için Regex'lerin kullanıldığı alanlardır. Bu bölümde Scanner sınıfı temelleri işlenmiştir, Regular Expression'ları başka bir başlıkta incelemeyi düşünüyorum.

Scanner sınıfı Object sınıfını extend, **Iterator** ve **Closeable** arayüzlerini implemente eder. Scanner sınıfını kullanabilmek için **``java.util.Scanner``**
paketini import etmemiz gerekir.

**``Not:``** Scanner sınıfı harici senkronizasyon olmadan **multithreaded** kullanım için güvenli değildir.  

Paket tanımlamasından sonra Scanner sınfı ile veri okuyabilmek için öncelikle bu sınıftan bir nesne oluşturmak gerekir.

```java
Scanner sc1 = new Scanner(InputStream input);
Scanner sc2 = new Scanner(File file);
Scanner sc3 = new Scanner(String str);
```

- ``Standard Input Stream:`` Yapıcı metoda **System.in** parametresi geçilerek, **konsol** aracılığıyla klavyeden veri almak için kullanılır.
- ``File:`` Dosyadan veri okumak için kullanılır. **I/O Operations** konusundan işlenecektir.
-  ``String:`` Girdi değerini **String** tipinde bir değişkenden okumak için kullanılır. 

#### Klavyeden Veri Okuma Örneği

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {
    
        Scanner input = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = input.nextLine();
        System.out.println("My name is " + name);
        
        input.close();
    }
}
```

Output:
```
Enter your name: Barış
My name is Barış
```
<br>

## Scanner Sınıfı Metotları

Aşağıdaki tabloda Scanner sınıfının temel metotları yer almaktadır. Scanner sınıfı farklı tipte input'ları okuyabilmek için çeşitli metotlar sağlar.

| Method | Exceptions |
|:--------:|:------------:|
| void close() | - |
| boolean hasNext() | ``IllegalStateException`` |
| boolean hasNext?(int radix) | ``IllegalStateException`` <br> ``IllegalArgumentException`` |
| Pattern delimiter() | - |
| nextByte(int radix) | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` <br> ``IllegalArgumentException`` |
| nextShort(int radix) | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` <br> ``IllegalArgumentException`` |
| nextInt(int radix) | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` <br> ``IllegalArgumentException`` |
| nextLong(int radix) | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` <br> ``IllegalArgumentException`` |
| nextFloat() | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` | 
| nextDouble() | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` |
| nextBoolean() | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` |
| nextBigInteger(int radix) | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` <br> ``IllegalArgumentException`` |
| nextBigDecimal() | ``InputMismatchException`` <br> ``NoSuchElementException`` <br> ``IllegalStateException`` |
| next() | ``NoSuchElementException`` <br> ``IllegalStateException`` |
| nextLine() | ``NoSuchElementException`` <br> ``IllegalStateException`` |

<br>

* **InputMismatchException:** Input içinde sonraki değer, veri tipi ile eşleşmezse veya kapsamı dışına çıkarsa fırlatılır.
* **NoSuchElementException:** Input içinde okunacak veri kalmadıysa veya yoksa fırlatılır. 
* **IllegalStateException:** Scanner nesnesi kapatıldığı halde kullanılmaya çalışılırsa fırlatılır. 
* **IllegalArgumentException:** Belirtilen radix (taban) aralığı dışındaysa fırlatılır. 

## Java Scanner close() Metodu

``java.util.Scanner`` sınıfının bir metodu olan **close()**, açık olan Scanner nesnesini kapatmak için kullanılır. Eğer Scanner objesi daha önceden kapatılmışsa bu metodun çalıştırılması nesneyi etkilemez.

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "Scanner close() metodu için örnek program çalıştı.";

        Scanner input = new Scanner(sentence);
        try {

            System.out.println("> " + input.nextLine());
            input.close();
            System.out.println("\nScanner kapatıldı.\n");

            System.out.println("> Scanner nesnesi kullanılmaya çalışılıyor!");
            System.out.println(input.nextLine());

        } catch (Exception exception) {
            System.out.println("Hata: " + exception);
        }
    }
}
```

Output:
```
> Scanner close() metodu için örnek program çalıştı.

Scanner kapatıldı.

> Scanner nesnesi kullanılmaya çalışılıyor!
Hata: java.lang.IllegalStateException: Scanner closed
```

## Java Scanner hasNext() ve hasNext?() Metodu

``java.util.Scanner`` sınıfının bir metodu olan **hasNext()**, Scanner input içinde başka bir token'a sahipse ``true`` değilse ``false`` döner. Yani mevcut token'dan sonra başka bir token'ın olup olmadığını kontrol ediyor.  **hasNext?(radix)** metodu ise Scanner input'u içinde sonraki token'ın **``?``** olarak ifade edilen veri tipi olarak yorumlanıp yorumlanamayacığına karar vermek için kullanılır. Eğer metoda bir radix (taban) parametre geçilmediyse varsayılan olarak **decimal (ondalık) değer** kullanılır ve buna göre boolean bir değer döner. Bu konu ile ilgili örnekler nextInt() ve sonraki metotlarda işlenmiştir.

**``Not:``** Scanner bu iki metodu kullanırken token'lar arasında atlama/ilerleme yapmaz. Sadece kontrol amaçlı kullanılır.

## Java Scanner delimiter() Metodu

``java.util.Scanner`` sınıfının bir metodu olan **delimiter()**, Scanner sınıfının o anda kısıtlayıcı olarak kullandığı Pattern'i döndürür. Scanner sınıfında varsayılan kısıtlayıcı karakter boşluktur (whitespace) ancak **useDelimiter()** metoduyla bu karakteri değiştirebiliriz.

**Örnek 1:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "\"Write once run everywhere. \" ";
        Scanner input = new Scanner(sentence);

        System.out.println("Java Programming Language: " + input.nextLine());
        System.out.println("Delimiter: " + input.delimiter());
        
        input.close();
    }
}
```

Output:
```
Java Programming Language: "Write once run everywhere." 
Delimiter: \p{javaWhitespace}+
```

<br>

**Örnek 2:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {
    
        String sentence = "Java-Programming-Language";
        Scanner input = new Scanner(sentence);
        input.useDelimiter("-");
        System.out.println("Delimiter: " + input.delimiter());

        System.out.println("-- List --");
        
        while (input.hasNext())
            System.out.println(input.next());

        input.close();
    }
}
```

Output:
```
Delimiter: -
-- List --
Java
Programming
Language
```

## Java Scanner nextInt() Metodu

``java.util.Scanner`` sınıfının bir metodu olan **nextInt(radix)**, sonraki token'ı input içinden int olarak okur. Çevirme işlem başarılıysa Scanner sonraki token'a geçer. Eğer metoda bir radix (taban) parametre geçilmediyse varsayılan olarak **decimal (ondalık) değer** kullanılır ve bu radix parametresine göre bir tam sayı döner.

- ASCII karakterlerine [buradan](https://tr.wikipedia.org/wiki/ASCII) ulaşabilirsiniz.

**Örnek 1:**

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "GitHub 7 + 15 = 22.0";
        Scanner input = new Scanner(sentence);

        while (input.hasNext()) {
            if (input.hasNextInt()) // decimal için kontrol yapar
                System.out.println("Tam sayı değeri bulundu: " + input.nextInt() + " ✔"); // decimal
            else
                System.out.println("Tam sayı değeri bulunamadı: " + input.next() + " ✗");
        }

        input.close();
    }
}
```

Output:
```
Tam sayı değeri bulunamadı: GitHub ✗
Tam sayı değeri bulundu: 7 ✔
Tam sayı değeri bulunamadı: + ✗
Tam sayı değeri bulundu: 15 ✔
Tam sayı değeri bulunamadı: = ✗
Tam sayı değeri bulunamadı: 22.0 ✗
```

<br>

**Örnek 2:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "GitHub 07 + 0F = 22.0";
        Scanner input = new Scanner(sentence);

        while (input.hasNext()) {
            if (input.hasNextInt(16)) // hexadecimal için kontrol yapar
                System.out.println("Tam sayı değeri bulundu: " + input.nextInt(16) + " ✔"); // hexadecimal
            else
                System.out.println("Tam sayı değeri bulunamadı: " + input.next() + " ✗");
        }

        input.close();
    }
}
```

Output:
```
Tam sayı değeri bulunamadı: GitHub ✗
Tam sayı değeri bulundu: 7 ✔
Tam sayı değeri bulunamadı: + ✗
Tam sayı değeri bulundu: 15 ✔
Tam sayı değeri bulunamadı: = ✗
Tam sayı değeri bulunamadı: 22.0 ✗
```
Yukarıdaki örnekte **hasNextInt()** metoduna radix parametresi geçilmeseydi ``07`` ve ``0F`` değerleri if koşuluna girmeyerek else koşulunda yazılacaktı.

<br>

**Örnek 3:** InputMismatchException <br>
Aşağıdaki örnekte input içinde okunan değer tam sayıya yorumlanamayacağı için hata fırlatıldı.

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        try {
            String sentence = "GitHub 7 + 15 = 22.0";
            Scanner input = new Scanner(sentence);

            while (input.hasNext())
                System.out.println("Tam sayı değeri bulundu: " + input.nextInt());

            input.close();
        } catch (Exception exception) {
            System.out.println("Hata: " + exception);
        }
    }
}
```

Output: 
```
Hata: java.util.InputMismatchException
```

<br>

**Örnek 4:** NoSuchElementException
Aşağıdaki örnekte input içindeki token okunduktan sonra başka token olmamasına rağmen döngü çalıştığı için hata fırlatıldı.

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        try {
            String sentence = "GitHub";
            Scanner input = new Scanner(sentence);

            for (int i = 0; i < 3; i++)
                if (input.hasNextInt())
                    System.out.println("Tam sayı değeri bulundu: " + input.nextInt());
                else
                    System.out.println("Tam sayı değeri bulunamadı: " + input.next());
            input.close();
        } catch (Exception exception) {
            System.out.println("Hata: " + exception);
        }
    }
}
```

Output:
```
Tam sayı değeri bulunamadı: GitHub
Hata: java.util.NoSuchElementException
```

<br>

**Örnek 5:** IllegalStateException
**close()** metodunda yaptığımız örneğe benzer şekilde, aşağıdaki örnekte Scanner nesnesine kapatılmış olmasına rağmen ulaşılmaya çalışıldığı için hata fırlatıldı.

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        try {
            String sentence = "GitHub";
            Scanner input = new Scanner(sentence);

            input.close();
            System.out.println("Scanner kapatıldı.");
            System.out.println("> Scanner nesnesi kullanılmaya çalışılıyor!");

            while (input.hasNext())
                if (input.hasNextInt())
                    System.out.println("Tam sayı değeri bulundu: " + input.nextInt());
                else
                    System.out.println("Tam sayı değeri bulunamadı: " + input.next());

            input.close(); // bir etkisi yok
        } catch (Exception exception) {
            System.out.println("Hata: " + exception);
        }
    }
}
```

Output:
```
Scanner kapatıldı.
> Scanner nesnesi kullanılmaya çalışılıyor!
Hata: java.lang.IllegalStateException: Scanner closed
```

<br>

**Örnek 6:** IllegalArgumentException

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        try {
            String sentence = "GitHub 07 + 0F = 22.0";
            Scanner input = new Scanner(sentence);

            while (input.hasNext()) {
                if (input.hasNextInt(598670))
                    System.out.println("Tam sayı değeri bulundu: " + input.nextInt(598670) + " ✔");
                else
                    System.out.println("Tam sayı değeri bulunamadı: " + input.next() + " ✗");
            }

            input.close();
        } catch (Exception exception) {
            System.out.println("Hata: " + exception);
        }
    }
}
```

Output: 
```
Hata: java.lang.IllegalArgumentException: radix:598670
```

## Java Scanner nextDouble() Metodu

``java.util.Scanner`` sınıfının bir metodu olan **nextDouble()**, sonraki token'ı input içinden double olarak okur. Çevirme işlem başarılıysa Scanner sonraki token'a geçer.

**Örnek:**

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "GitHub 7 + 15 = 22.0";
        Scanner input = new Scanner(sentence);

        while (input.hasNext()) {
            if (input.hasNextDouble())
                System.out.println("Double değeri bulundu: " + input.nextDouble() + " ✔");
            else
                System.out.println("Double değeri bulunamadı: " + input.next() + " ✗");
        }

        input.close();
    }
}
```

Output:
```
Double değeri bulunamadı: GitHub ✗
Double değeri bulundu: 7.0 ✔
Double değeri bulunamadı: + ✗
Double değeri bulundu: 15.0 ✔
Double değeri bulunamadı: = ✗
Double değeri bulundu: 22.0 ✔
```
- InputMismatchException, NoSuchElementException ve IllegalStateException örnekleri için **``nextInt()``** metodu incelenebilir.

 
## Java Scanner nextBoolean() Metodu
``java.util.Scanner`` sınıfının bir metodu olan **nextBoolean()**, sonraki token'ı input içinden boolean olarak okur. Çevirme işlem başarılıysa Scanner sonraki token'a geçer. Boolean değeri okunurken "to lower cast" işlemi uygulanır.

**Örnek:**

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "7 > 15 ? TRUE : False";
        Scanner input = new Scanner(sentence);

        while (input.hasNext()) {
            if (input.hasNextBoolean())
                System.out.println("Boolean değeri bulundu: " + input.nextBoolean() + " ✔");
            else
                System.out.println("Boolean değeri bulunamadı: " + input.next() + " ✗");
        }
        input.close();
    }
}
```

Output:
```
Boolean değeri bulunamadı: 7 ✗
Boolean değeri bulunamadı: > ✗
Boolean değeri bulunamadı: 15 ✗
Boolean değeri bulunamadı: ? ✗
Boolean değeri bulundu: true ✔
Boolean değeri bulunamadı: : ✗
Boolean değeri bulundu: false ✔
```
- InputMismatchException, NoSuchElementException ve IllegalStateException örnekleri için **``nextInt()``** metodu incelenebilir.


## Java Scanner nextBigInteger() ve nextBigDecimal() Metotları

``java.util.Scanner`` sınıfı metotlarından **nextBigInteger(radix)** metodu sonraki token'ı input içinden BigInteger olarak okurken, **nextBigDecimal()** metodu ise BigDecimal olarak okur. Çevirme işlem başarılıysa Scanner sonraki token'a geçer. nextBigInteger() metodu için eğer bir radix (taban) parametre geçilmediyse varsayılan olarak **decimal (ondalık) değer** kullanılır ve bu radix parametresine göre bir tam sayı döner.

```java
import java.math.BigDecimal;
import java.math.BigInteger;
import java.util.Scanner;

public class Driver {
  public static void main(String[] args) {
  
        Scanner input = new Scanner(System.in);
        System.out.print("Enter a big integer: ");
        BigInteger bigIntegerValue = input.nextBigInteger();
        System.out.println("Using nextBigInteger(): " + bigIntegerValue);

        System.out.print("Enter a big decimal: ");

        BigDecimal bigDecimalValue = input.nextBigDecimal();
        System.out.println("Using nextBigDecimal(): " + bigDecimalValue);

        input.close();
  }
}
```

Output:
```
Enter a big integer: 987654321
Using nextBigInteger(): 987654321
Enter a big decimal: 97531.246810
Using nextBigDecimal(): 97531.24681
```
- InputMismatchException, NoSuchElementException, IllegalStateException ve IllegalArgumentException örnekleri için **``nextInt()``** metodu incelenebilir.


## Java Scanner next() Metodu

``java.util.Scanner`` sınıfının bir metodu olan **next()**, input içindeki complete token'ları **boşluk (" ")** karakteri ile karşılaşana kadar okur ve String tipinde döner (boşluk/delimiter karakteri dahil **değildir**).

**``Not:``** Complete token, input içinde diğer token'lardan önce gelen ve kendisinden sonra delimiter deseniyle eşleşen token'dır.

**Örnek 1:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "GitHub, yazılım geliştirme ve " +
              "sürüm kontrolü için kullanılan web tabanlı bir hosting sağlayıcısıdır.";
        int count = 0;
        Scanner input = new Scanner(sentence);

        System.out.println(":- Kelime Listesi -:" + "\n" + "--------------------");

        while (input.hasNext()) {
            System.out.println(input.next());
            count++;
        }

        System.out.println("-----------------" + "\n" + "Kelime sayısı: " + count);
        System.out.println("Delimiter: " + input.delimiter());
        input.close();
    }
}
```

Output:
```
:- Kelime Listesi -:
--------------------
GitHub,
yazılım
geliştirme
ve
sürüm
kontrolü
için
kullanılan
web
tabanlı
bir
hosting
sağlayıcısıdır.
-----------------
Kelime sayısı: 13
Delimiter: \p{javaWhitespace}+
```

Yukarıdaki örnekte default delimiter olarak boşluk karakteri kullanıldı ancak **useDelimiter()** metoduyla delimiter'ı **"/"** (forward slash) karakteri gibi herhangi bir karakterle değiştirip, kelimeleri bu yeni delimiter'a göre listeleyebilirdik.

<br>

**Örnek 2:** NoSuchElementException

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        try {
            String sentence = " ";
            Scanner input = new Scanner(sentence);

            System.out.println(input.next());
            input.close();

        } catch (Exception exception) {
            System.out.println("Hata: " + exception);
        }
    }
}
```

Output:
```
Hata: java.util.NoSuchElementException
```
<br>

**Örnek 3:** IllegalStateException

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        try {
            String sentence = "What is the difference between Git and Github?";

            Scanner input = new Scanner(sentence);
            input.close();
            
            System.out.println("Scanner kapatıldı!");

            System.out.println(input.next());
            input.close();

        } catch (Exception exception) {
            System.out.println("Hata: " + exception);
        }
    }
}
```

Output:
```
Scanner kapatıldı!
Hata: java.lang.IllegalStateException: Scanner closed
```

## Java Scanner nextLine() Metodu

``java.util.Scanner`` sınıfının bir metodu olan **nextLine()**, next() metodunun aksine cümleyi **end of line karakteri** (\n - line separator) ile karşılaşıncaya kadar okur. Başka bir deyişle, metin içinde cümle yeni satırda tanımlanıyorsa veya cümle sonunda "\n" karakteri yer alıyorsa metot bu değeri String tipinde döner ve bu seperator'dan sonra gelen satıra geçer. Değeri konsoldan alırken **enter** tuşuna bastığımızda bu karakter otomatik olarak String ifadenin sonuna eklenir. 

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        String sentence = "✔ GitHub, yazılım geliştirme ve sürüm kontrolü için kullanılır.\n" +
                "✔ Web tabanlı bir hosting sağlayıcısıdır.";
        int count = 0;
        Scanner input = new Scanner(sentence);

        System.out.println(":- Github Nedir?");

        while (input.hasNextLine()) {
            System.out.println(input.nextLine());
            count++;
        }

        System.out.println(":- Cümle sayısı: " + count);
        System.out.println("Delimiter: " + input.delimiter());
        input.close();
    }
}
```

Output:
```
:- Github Nedir?
✔ GitHub, yazılım geliştirme ve sürüm kontrolü için kullanılır.
✔ Web tabanlı bir hosting sağlayıcısıdır.
:- Cümle sayısı: 2
Delimiter: \p{javaWhitespace}+
```

**``Not:``** nextLine() metodunun kendisi hariç diğer ``next()`` ve ``nextFoo()`` (int, double, boolean vb.) metotlarında ortak bir problem vardır. Bu metotlar girilen değeri okuduktan sonra end of line karakterini okumadan imleci, okunan değerin hemen sonrasında bırakır. Bu tür metotlardan sonra nextLine() metodu kullanılırsa, herhangi bir input alınmadan sonraki satıra geçilir. Bunun nedeni, nextLine() metodunun imleçten sonraki "/n" karakterini okumasıdır.

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);
        System.out.println(":--- KANSAS Driver's License ---:");
        System.out.print("Lic No: ");
        String licNo = input.nextLine();
        System.out.print("Day of Birth: ");
        int dob = input.nextInt();
        System.out.print("Name: ");
        String name = input.nextLine();
        System.out.print("Surname: ");
        String surname = input.nextLine();
        System.out.println("---------------------------------");
        input.close();
    }
}
```

Output:
```
:--- KANSAS Driver's License ---:
Lic No: K12-34-5974
Day of Birth: 01121974
Name: Surname: Elizabeth
---------------------------------
```
Yukarıdaki örnekte görüldüğü gibi ``nextInt()`` metodundan sonra **name** değeri alınmadan **surname** değişkeni için tanımlanan ``nextLine()`` metoduna atlandı. ``dob`` değişkenine atanan değerden sonra kürsör aşağıdaki gibi bir konumda olduğu için nextLine() meotdu kullanıcıdan input almak yerine "\n" karakterini okudu ve işi sonraki nextLine() metoduna bıraktı.

```
Day of Birth: 01121974_\n // "_" karakteri kürsörü temsil ediyor.
```
- **Geçici Çözüm (Workaround)**

Böyle bir durumda ``next()`` ve ``nextFoo()`` metotlarından sonra end of line karakterini okuyup yeni satıra geçmek için araya **``nextLine()``** metodu yazılabilir.

```java
System.out.print("Day of Birth: ");
int dob = input.nextInt();
input.nextLine(); // "\n" karakterini okuyup yeni satıra geçer
        
System.out.print("Name: ");
String name = input.nextLine();
```
- **Kalıcı Çözüm**

Daha iyi bir çözüm ise alınacak tüm değerlerin **``nextLine()``** metoduyla **String** tipinde alıp ilgili tiplere çevirmektir (Parsing-Casting). Kodun bu yönteme göre düzenlenmiş hali aşağıda mevcuttur.

```java
import java.time.LocalDate;

public class Controller {
    private boolean isProperName(String name) { 

        int length = name.length();
        boolean control = false;

        if (Character.isUpperCase(name.charAt(0))) {
            control = true;

            for (int i = 1; i < length; i++) {
                if (Character.isLowerCase(name.charAt(i))) {
                    control = true;
                } else {
                    control = false;
                    break;
                }
            }
            return control;
        }
        return control;
    }

    public boolean checkNamingConvention(String name, String surname) {
    
	// Format: Name Surname, yani baş harfler büyük diğerleri küçük
        boolean resultForName = isProperName(name);
        boolean resultForSurname = isProperName(surname);

        if (resultForName == true && resultForSurname == true)
            return true;
        else
            return false;
    }

    public boolean checkAgeForLicence(String date) {
        if (date.length() == 8) {
            int year = Integer.parseInt(date) % 10000;

            int age = LocalDate.now().getYear() - year;

            if (age >= 16)
                return true;
            else
                return false;
        }
        return false;
    }
}
```

```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);
        Controller controller = new Controller();

        System.out.println(":--- KANSAS Driver's License Application ---:");
        System.out.println("Info: Initials must be uppercase letter.\n");
        System.out.print("Lic No: ");
        String licNo = input.nextLine();
        System.out.print("Day of Birth: ");
        String dob = input.nextLine();
        System.out.print("Name: ");
        String name = input.nextLine();
        System.out.print("Surname: ");
        String surname = input.nextLine();
        input.close();

        System.out.println("\nApplication is being evaluated...");

        if (controller.checkNamingConvention(name, surname) == false)
            System.out.println("Result: Denied ✗ \n" + "Reason: Spelling mistake");
        else if (controller.checkAgeForLicence(dob) == false)
            System.out.println("Result: Denied ✗\n" + "Reason: Your age is not eligible for a driver's license.");
        else
            System.out.println("Result: Accepted ✔");
    }
}
```

Output: 
```
:--- KANSAS Driver's License Application ---:
Info: Initials must be uppercase letter.

Lic No: K12-54-7824
Day of Birth: 21012007
Name: Caron
Surname: Elizabeth

Application is being evaluated...
Result: Denied ✗
Reason: Your age is not eligible for a driver's license.
```
- NoSuchElementException ve IllegalStateException örnekleri için **``next()``** metodu incelenebilir.


## Java Scanner Sınıfı ile İlgili Diğer Örnekler

**Örnek 1:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {
        
        Scanner veriAl = new Scanner(System.in);
        System.out.println("int tipinde veri girin:");
        int veri1 = veriAl.nextInt();
        System.out.println("String tipinde veri girin:");
        String veri2 = veriAl.next();
        System.out.println("boolean tipinde veri girin:");
        boolean veri3 = veriAl.nextBoolean();
        veriAl.close();
        System.out.print("Girilen değerler: " + veri1 + " - " + veri2 + " - " + veri3);
    }
}
```

Output:
```
int tipinde veri girin:
17
String tipinde veri girin:
Java
boolean tipinde veri girin:
False
Girilen değerler: 17 - Java - false
```
<br>

**Örnek 2:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        Scanner veriAl = new Scanner(System.in);
        System.out.print("Vize notunuzu giriniz: ");
        byte midtermExam = veriAl.nextByte();
        System.out.print("Final notunuzu giriniz: ");
        byte finalExam = veriAl.nextByte();
        veriAl.close();

        double average = ((midtermExam * 0.4) + (finalExam * 0.6));
        System.out.println("Ortalama: " + average);

        if (average > 50)
            System.out.println("> Dersi geçtiniz.");
        else
            System.out.println("> Dersten kaldınız.");
    }
}
```

Output:
```
Vize notunuzu giriniz: 85
Final notunuzu giriniz: 42
Ortalama: 59.2
> Dersi geçtiniz.
```
<br>

**Örnek 3:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        Scanner veriAl = new Scanner(System.in);
        int toplam;
        System.out.print("İlk tam sayıyı girin: ");
        int firstNumber = veriAl.nextInt();
        System.out.print("İkinci tam sayıyı girin: ");
        int lastNumber = veriAl.nextInt();
        System.out.print("Artış miktarı: ");
        int increase = veriAl.nextInt();
        veriAl.close();
        
        // increase = iki ardışık sayı arasındaki fark
        // ilk ve son değer toplama dahildir
        toplam = ((lastNumber + firstNumber) * (lastNumber - firstNumber + increase)) / (2 * increase);
        System.out.println("İki sayı arasındaki sayıların toplamı: " + toplam);
    }
}
```

Output:
```
İlk tam sayıyı girin: 3
İkinci tam sayıyı girin: 21
Artış miktarı: 2
İki sayı arasındaki sayıların toplamı: 120
```
<br>


**Örnek 4:**
```java
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        Scanner veriAl = new Scanner(System.in);
        int[][] array = new int[2][2];

        System.out.println(">-----< Matris Tablosu >-----<");
        System.out.print("1.satırın 1.sütununu girin: ");
        array[0][0] = veriAl.nextInt();
        System.out.print("1.satırın 2.sütununu girin: ");
        array[0][1] = veriAl.nextInt();
        System.out.print("2.satırın 1.sütununu girin: ");
        array[1][0] = veriAl.nextInt();
        System.out.print("2.satırın 2.sütununu girin: ");
        array[1][1] = veriAl.nextInt();
        veriAl.close();
        System.out.println("\nSonuç: \n");

        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 2; j++) {
                System.out.print("[" + array[i][j] + "]\t");
            }
            System.out.println(" ");
        }
    }
}
```

Output:
```
>-----< Matris Tablosu >-----<
1.satırın 1.sütununu girin: 3
1.satırın 2.sütununu girin: 5
2.satırın 1.sütununu girin: 7
2.satırın 2.sütununu girin: 9

Sonuç: 

[3]	[5]	 
[7]	[9]	
```
<br>


**Örnek 5:**
```java
import java.util.Random;
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {

        int count = 1;
        Scanner veriAl = new Scanner(System.in);
        Random r = new Random();
        int sayi = r.nextInt(10);

        while (true) {
            System.out.println("Tahmin Girin (0 - 10): ");
            int tahmin = veriAl.nextInt();

            if (tahmin == sayi) {
                System.out.println("Sonuç: " + count + ". tahminde bildiniz.");
                break;
            } else
                count++;
        }
        veriAl.close();
    }
}
```

Output:
```
Tahmin Girin (0 - 10): 
5
Tahmin Girin (0 - 10): 
7
Tahmin Girin (0 - 10): 
9
Sonuç: 3. tahminde bildiniz.
```

Bu sınıf hakkında daha fazla bilgi almak için [Oracle API Doc.](https://docs.oracle.com/javase/8/docs/api/index.html?java/util/Scanner.html) veya [TutorialsPoint](https://www.tutorialspoint.com/java/util/java_util_scanner.htm)'i inceleyebilirsiniz.
