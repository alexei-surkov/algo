```java
// Given the array of integers nums, you will choose two different indices i and j of that array. Return the maximum value of (nums[i]-1)*(nums[j]-1).

public class Solution {
// Идея - найти два наибольших числа в массиве. Соответственно, их произведение будет максимальным
public int maxProduct(int[] nums) {
int max1 = Integer.MIN_VALUE;
int max2 = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > max1) {
                max2 = max1;
                max1 = nums[i];
                continue;
            }
            if (nums[i] > max2) {
                max2 = nums[i];
            }
        }
        
        return (max1 - 1) * (max2 - 1);
    }
}
```

### Ошибки
В ветке, когда очередное значение больше максимума max1, перепутал местами инструкции присвоения,
из-за этого в max1 и max2 было одинаковое значение