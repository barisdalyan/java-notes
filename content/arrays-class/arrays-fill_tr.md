## Arrays.fill Metodu

Bir dizinin belirli bir bölümüne veya tamamına **``Arrays``** sınıfının **``fill()``** metodu ile değer atayabiliriz. Bu metot, kendisine verilen değeri dizinin tüm elemanlarına veya belirli indisler arasındaki elemanlara atar.

```java
import java.util.Arrays;  
  
public class ArraysFill {  
    public static void main(String[] args) {  
  
        // Arrays.fill(Object[] array, Object value) dizinin tamamını value ile doldurur.  
	// Arrays.fill(Object[] array, int başlangıç indisi, int bitiş indisi (dahil değil), Object value);  
	
	int[] array1 = {0, 0, 0, 0, 0};  
        int[] array2 = {1, 1, 1, 1, 1};  
  
        Arrays.fill(array1, 1);  
        Arrays.fill(array2, 2, 4, 0);  
  
        System.out.print("İlk dizi: ");  
        for (int countArray1 : array1)  
            System.out.print(countArray1);  
  
  
        System.out.print("\nİkinci dizi: ");  
        for (int countArray2 : array2)  
            System.out.print(countArray2);  
    }  
}
```

Output:
```
İlk dizi: 11111
İkinci dizi: 11001
```


