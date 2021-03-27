## Arrays.equals Metodu

Dizilerde karşılaştırma işlemi **``Arrays``** sınıfının **``equals()``** metodu ile yapılabilir. Dizilerin eşit olabilmesi için **eleman sayıları** ve **elemanları** aynı olmalıdır.  Karşılaştırma işlemi için dizilerin aynı tipte olaması gerekir: Object, String, boolean, char, byte, int, short, long, float, double.
```java
import java.util.Arrays;

public class CompareArrays {
    public static void main(String[] args) {

        // Arrays.equals(array1, array2);
  
        char[] array1 = {'t', 'r'};
        char[] array2 = {'r', 't'};
        System.out.println("Sonuç: " + Arrays.equals(array1, array2));
    }
}
```

Output:
```
Sonuç: false
```


