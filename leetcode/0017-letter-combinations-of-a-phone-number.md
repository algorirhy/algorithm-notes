# [电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

```java
class Solution {

    String[] letter_map = {" ","*","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    List<String> res = new ArrayList<>();

    public List<String> letterCombinations(String digits) {
        if(digits == null || digits.length() == 0)
            return res;
        iterStr(digits, "", 0);
        return res;
    }

    private void iterStr(String str, String letter, int index){
        if(index == str.length()){
            res.add(letter);
            return;
        }
        char c = str.charAt(index);
        int pos = c - '0';
        String map_string = letter_map[pos];
        for(int i = 0; i < map_string.length(); i++){
            iterStr(str, letter+map_string.charAt(i), index+1);
        }
    }
}
```