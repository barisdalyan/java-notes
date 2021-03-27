##  Arrays.binarySearch Metodu

Java'da, diziler içinde **``Arrays``** sınıfının **``binarySearch()``** metodu ile arama işlemi yapılabilir. Metot, aranan elemanı bulursa indisini döner. Eğer bulamazsa negatif değer (-1) döner. Dizilerde ikili arama yapabilmek için dizinin sıralı olması gerekir. Sıralama yapmak için **``Arrays.sort()``** metodu kullanılabilir. Metot, eleman indisini yeni dizi sırasına göre döndürülür.

```java
import java.util.Arrays;

public class SearchInArrays {
    public static void main(String[] args) {

        int[] array = {3, 4, 12, 9, 2, 5};

        Arrays.sort(array); // Önce dizi sıralanır. (küçükten-büyüğe)
        System.out.println(Arrays.toString(array));
        int value = Arrays.binarySearch(array, 12); // Aranan eleman: 12

        if (value < 0)
            System.out.println("Eleman bulunamadı.");
        else
            System.out.println("Eleman indisi: " + value);
    }
}
```

Output:
```
[2, 3, 4, 5, 9, 12]
Eleman indisi: 5
```


