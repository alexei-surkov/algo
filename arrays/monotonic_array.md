```java
// An array is monotonic if it is either monotone increasing or monotone decreasing.
//An array nums is monotone increasing if for all i <= j, nums[i] <= nums[j]. An array nums is monotone decreasing if for all i <= j, nums[i] >= nums[j].
//Given an integer array nums, return true if the given array is monotonic, or false otherwise.


// Идея: сначала вычисляем паттерн (убывание или возрастание): 
// 1) Берем первые 2 уникальных элемента массива
// 2) На их основе понимаем - убывающий он или возрастающий. 
// Если убывающий - нужно проверять, что каждый следующий элемент меньше или равен предыдущему
// Если возрастающий - проверяем, что каждый элемент больше или равен предыдущему

// Сложность по времени O(n), n - длина входного массива
// Сложность по памяти О(1)
  

public class Solution {
    public boolean isMonotonic(int[] nums) {
        String order = "";
        int prevValue = nums[0];
        for (int i = 1; i < nums.length; prevValue = nums[i], i++) {
            if ("asc".equals(order)) {
                if (nums[i] < prevValue) {
                    return false;
                }
            } else if ("desc".equals(order)) {
                if (nums[i] > prevValue) {
                    return false;
                }
            } else {
                if (nums[i] > prevValue) {
                    order = "asc";
                } else if (nums[i] < prevValue) {
                    order = "desc";
                }
            }
        }
        return true;
    }
}
```

Ошибок не было