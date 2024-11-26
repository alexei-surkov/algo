```java
// Идея: собрать из двух строк карты, где ключ - буква, значение - количество этой буквы в слове. 
// Далее - перевернуть карту K-V --> V-K. Если размерность мапы будет совпадать и все ключи из мапы 1
// будут содержаться в мапе 2, то строка будет являться изоморфной
// В качестве не асимптотической оптимизации предлагаю в начале алгоритма проверять длину первой и второй строки. В случае
// несовпадения - сразу вернуть false

// Асимптотика: O(n) - память (2 новых карты, 2 новых множества); O(n) - время (наполнение карта и множеств, сравнение множеств)

// Решение неправильное. 

// !!!! Неправильно понял условие и неправильно решил!!!!


class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) { // Проговорил про оптимизацию, но сразу не написал
            return false;   
        }
        
        Map<Character, Integer> sMap = toCharCountMap(s); // возникла идея вынести преобразование в карту отдельным методом, чтобы не дублировать код
        Map<Character, Integer> tMap = toCharCountMap(t);
        
        // Не асимптотическая оптимизация - проверить длину карт и вернуть false если не совпадает
        if (sMap.size() != tMap.size()) {
            return false;
        }
        
        // Значения карты преобразовываем в Set и сравниваем эквивалентность
        Set<Integer> sValuesSet = new HashSet<>(sMap.values());
        Set<Integer> tValuesSet = new HashSet<>(tMap.values());
        return sValuesSet.equals(tValuesSet);
        
    }
    
    private Map<Character, Integer> toCharCountMap(String source) {
        Map<Character, Integer> result = new HashMap<>();
        for (char c : source.toCharArray()) {
            result.merge(c, 1, (was, now) -> was + 1);
        }
        return result;
    }
}
```

### Ошибки
1. Синтаксических ошибок допущено не было, но решение неверное в целом
2. Главная ошибка - некорректное решение из-за того, что невнимательно прочитал условие

Код решения после просмотра видео-разбора

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        char[] sChars = s.toCharArray();
        char[] tChars = t.toCharArray();

        // Не асимптотическая оптимизация
        if (sChars.length != tChars.length) {
            return false;
        }

        Map<Character, Character> sMap = new HashMap<>();
        Map<Character, Character> tMap = new HashMap<>();

        for (int i = 0, length = sChars.length; i < length; i++) {
            if (sMap.containsKey(sChars[i])) { // containsKey, а не contains
                if (sMap.get(sChars[i]) != tChars[i]) {
                    return false;
                }
            }
            sMap.put(sChars[i], tChars[i]);

            if (tMap.containsKey(tChars[i])) { // пропустил скобку
                if (tMap.get(tChars[i]) != sChars[i]) {
                    return false;
                }
            }
            tMap.put(tChars[i], sChars[i]);
        }
        return true;
    }
}
```

### Ошибки
1. Пропустил скобку (ошибка компиляции)
2. Проверку ключа в мапе написал как `contains`, а не `containsKey` - ошибка компиляции