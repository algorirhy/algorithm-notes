# [有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

```java
class Solution {
    private static final Map<Character, Character> map = new HashMap<>() {{
        put('{','}'); put('[',']'); put('(',')'); put('?','?');
        }};

    public boolean isValid(String s) {
        if (s.length() > 0 && !map.containsKey(s.charAt(0)))
            return false;
        LinkedList<Character> stack = new LinkedList<Character>() {{ add('?'); }};
        for (Character c : s.toCharArray()) {
            if (map.containsKey(c)) {
                stack.addLast(c);
            } else if (map.get(stack.removeLast()) != c) {
                return false;
            }
        }
        return stack.size() == 1;
    }
}
```

