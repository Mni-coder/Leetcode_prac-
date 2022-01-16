

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
