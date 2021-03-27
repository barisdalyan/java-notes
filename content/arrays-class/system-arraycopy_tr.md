## System.arraycopy Metodu

Bir diziyi, **``System``** sınıfının **``arraycopy()``** metodu ile başka bir diziye kopyalayabiliriz. Eğer hedef dizi boş değilse kopya değerler, hedefin üzerine yazılır.
```java
public class SystemArrayCopy {  
    public static void main(String[] args) {  
  
        // System.arraycopy(kaynak dizi, k. dizi başlangıç indisi, hedef dizi, h. dizi başlangıç indisi, adet);  
  
	int[] array1 = {1, 3, 5, 7, 9};  
        int[] array2 = new int[3];  
        int[] array3 = {2, 4, 6, 8};  
  
        System.arraycopy(array1, 0, array2, 0, 3);  
        System.arraycopy(array1, 0, array3, 1, 2);  
  
        System.out.print("Dizi-2 üyeleri: ");  
        for (int countArray : array2)  
            System.out.print(countArray + " ");  
  
        System.out.print("\nDizi-3 üyeleri: ");  
        for (int countArray : array3)  
            System.out.print(countArray + " ");  
    }  
}
```

Output:
```
Dizi-2 üyeleri: 1 3 5 
Dizi-3 üyeleri: 2 1 3 8 
```


