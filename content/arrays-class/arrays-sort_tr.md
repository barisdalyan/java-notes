##  Arrays.sort Metodu

Dizilerde küçükten büyüğe sıralama işlemi yapmak için **``Arrays``** sınıfının **``sort()``** metodu kullanılabilir. 

```java
import java.util.Arrays;

public class ArraysSort {
    public static void main(String[] args) {

        int[] array = {1, 7, 5, 9, 3, 2};

        Arrays.sort(array);

        System.out.print("Dizi üyeleri: ");
        for (int countArray : array) {
            System.out.print(countArray + " ");
        }

        ////////////////////////////////////////////////////


        // Arrays.sort(array, başlangıç indisi, bitiş indisi (sıralamaya dahil değil));
        // Dizinin istenilen aralığını sıralamak için kullanılır.

        int[] array2 = {13, 76, 65, 12, 14, 26, 58};

        Arrays.sort(array2, 0, 5);

        System.out.print("\nDizi-2 üyeleri: ");
        for (int countArray : array2) {
            System.out.print(countArray + " ");
        }
    }
}
```

Output:
```
Dizi üyeleri: 1 2 3 5 7 9 
Dizi-2 üyeleri: 12 13 14 65 76 26 58 
```


