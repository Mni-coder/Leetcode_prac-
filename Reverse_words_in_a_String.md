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