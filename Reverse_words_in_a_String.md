### Reverse Words in a String
Question：

Given an input string s, reverse the order of the words.
A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.
Return a string of the words in reverse order concatenated by a single space.

Example 1:

Input: s = "the sky is blue"
Output: "blue is sky the"

Example 2:

Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.

Example 3:

Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.

Constraints:

1 <= s.length <= 104
s contains English letters (upper-case and lower-case), digits, and spaces ' '.
There is at least one word in s.

URC--https://leetcode.com/problems/reverse-words-in-a-string/

```
class Solution {
public:
    string ReverseSentence(string str) {
        stack<char> st;
        string res = "";
        if(str == "") return str;
        for(int i= str.size()-1; i>=0;i--)
        {
            if(str[i] !=' ')
            {st.push(str[i]);}
            if(str[i] == ' ' || i == 0)
            {
                int ok = 0;
                while(!st.empty())
                {
                    res.push_back(st.top());
                    st.pop();
                    ok =1;
                }
                if(ok) res += ' ';
            }
        }
        return res.substr(0,res.size()-1);
    }
};
```