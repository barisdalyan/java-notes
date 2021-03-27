## Arrays.asList Metodu

Dizi içeriğini, **``Arrays``** sınıfının **``asList()``** metodu yardımıyla bir liste yapısına aktarabiliriz. Metot parametre olarak dizi alır ve geriye bir liste döner. 

```java
import java.util.Arrays;
import java.util.List;

public class ArraysAsList {
    public static void main(String[] args) {

        String[] array1 = {"Denizli", "İstanbul", "İzmir", "Aydın"}; // diziler oluşturuldu.
        Integer[] array2 = {20, 34, 35, 9}; // wrapper sınıf kullanılmalı: Integer, Float, Double vs.

        List myList1 = Arrays.asList(array1); // diziler asList() metodu ile liste yapısına dönüştü.
        List myList2 = Arrays.asList(array2);

        System.out.println(myList1);
        System.out.println(myList1.get(3));
        System.out.println(myList2);
        System.out.println(myList2.get(0));
    }
}
```
Output: 
```
[Denizli, İstanbul, İzmir, Aydın]
Aydın
[20, 34, 35, 9]
20
```


