## Arrays.copyOf Metodu

Bir diziyi, **``Arrays``** sınıfının **``copyOf()``** metodu yardımıyla başka bir diziye kopyalayabiliriz. Metot iki parametre alır ve geriye bir **dizi** döner. İlk parametre kopyalanacak dizidir, ikinci parametre ise diziden ne kadar eleman kopyalanacağını belirten bir tam sayı değeridir.

```java
import java.util.Arrays;  
  
public class ArraysCopyOf {  
    public static void main(String[] args) {  
  
        // Arrays.copyOf(array, kopyalanacak eleman sayısı);  
  
	char[] array = {'J', 'a', 'v', 'a', '-', '1', '1'};  
        char[] newArray;  
  
        System.out.print("Kopyalanacak dizi: ");  
        for (char countArray : array) 
            System.out.print(countArray);  
  
        newArray = Arrays.copyOf(array, 4);  
  
        System.out.print("\nYeni dizi: ");  
        for (char countNewArray : newArray)  
            System.out.print(countNewArray);  
    }  
}
```

Output:
```
Kopyalanacak dizi: Java-11
Yeni dizi: Java
```
<br>

Bu metot dışında **``Arrays``** sınıfının kopyalama işlemi yapan diğer bir metodu **``copyOfRange()``**, daha spesifik işlemler yapmak için kullanılır. Bu metot üç parametre alır. İlk parametre kopyalanacak kaynak diziyi belirtir, ikinci parametre dizinin hangi elemandan itibaren kopyalanmaya başlanacağını belirtir. Son parametre ise dizinin kaçıncı elemanına kadar kopyalama işlemine devam edileceğini belirtir.

```java
import java.util.Arrays;  
  
public class ArraysCopyOfRange {  
    public static void main(String[] args) {  
  
        // Arrays.copyOfRange(array, kaynak dizinin başlangıç indisi (dahil), bitiş indisi (dahil değil));  
  
	int[] array = {14, 53, 19, 23, 20, 12};  
        int[] newArray;  
  
        System.out.print("Kopyalanacak dizi: ");  
        for (int countArray : array) {  
            System.out.print(countArray);  
        }  
  
        newArray = Arrays.copyOfRange(array, 2, 4);  
  
        System.out.print("\nYeni dizi: ");  
        for (int countNewArray : newArray)  
            System.out.print(countNewArray);  
    }  
}
```

Output:
```
Kopyalanacak dizi: 145319232012
Yeni dizi: 1923
```

