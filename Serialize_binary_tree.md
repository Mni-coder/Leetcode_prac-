### Serialize and Deserialize Binary Tree

Question:
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

URC--https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

        struct TreeNode {
        int val;
        struct TreeNode *left;
        struct TreeNode *right;
        TreeNode(int x) :
                val(x), left(NULL), right(NULL) {
        }
    };
    
    class Solution {
    public:
        void inorder(TreeNode *root, string& ret){    
            if(root == nullptr){    
                ret += "#";
                return;
            }
        ret += to_string(root->val) + "!";    // "val" + "!"
        inorder(root->left, ret);   
        inorder(root->right, ret);    
    }
    
    char* Serialize(TreeNode *root) {    
        string ret;
        inorder(root, ret);
        char* ans = new char[ret.size() + 1];   
        strcpy(ans, ret.c_str());    
        return ans;    
    }
    
    TreeNode* deserialize(char *str, int& p){
        if(str[p] == '#'){   
            ++p;   
            return nullptr;
        }
    
        bool sign = 1;   
        if(str[p] == '-') sign = 0, ++p;    
        int val = 0;    
        while(str[p] != '!'){    
            val = val * 10 + str[p] - '0';
            ++p;
        }
        if(!sign) val = -val;   
        ++p;   
        TreeNode* root = new TreeNode(val);   
        root->left = deserialize(str, p);      
        root->right = deserialize(str, p);     
    
        return root;   
    }
    
    TreeNode* Deserialize(char *str) {
        int p = 0;    
        return deserialize(str, p);
    }
    };
