https://leetcode.com/problems/word-ladder/

```c++
// 每次更改单词一个位置的字符，然后使用 set 帮助我们查询是否存在
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> dict(wordList.begin(), wordList.end());
        if (dict.find(endWord) == dict.end()) return 0;
        unordered_set<string> us1 { beginWord };
        unordered_set<string> us2 { endWord };
        
        int step = 1;
        while (!us1.empty() && !us2.empty()) {
            ++step;
            if (us1.size() > us2.size()) swap(us1, us2); // 每次从小的 set 集合进行操作
            unordered_set<string> tmpSet;
            for (string word : us1) { // 针对集合中的每一个单词进行尝试
                for (int i = 0, len = word.size(); i < len; ++i) { // 针对每一个单词的每一个位置进行尝试
                    char ch = word[i];
                    for (int c = 'a'; c <= 'z'; ++c) { // 尝试换成 a-z 其中一个
                        word[i] = c;  // 记录该位置原先字符
                        if (us2.find(word) != us2.end()) return step; // 在另外一个集合中找到，返回 step
                        if (dict.find(word) != dict.end()) { // 另一个集合中没找到，在字典中找到
                            tmpSet.insert(word);
                            dict.erase(word);
                        }
                    }
                    word[i] = ch;     // 一轮尝试完毕，还原，保证除下一次更改位置外，其他位置不会有变化
                }
            }
            us1 = tmpSet;
        }
        
        return 0;
    }
};
```

