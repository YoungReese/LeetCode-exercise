https://leetcode.com/problems/throne-inheritance/

```c++
// 通过 map 和 vector 实现
// O(n)
class Person{
public:
    string name;
    vector<Person*> children;
    bool alive;
    Person(string& _name){
        alive = true;
        name = _name;
    }
};
class ThroneInheritance {
private:
    Person* king;
    map<string, Person*> m;
    
    void dfs(Person* curr, vector<string>& res){
        if(curr->alive) res.push_back(curr->name);
        for(int i = 0; i < curr->children.size(); i++){
            dfs(curr->children[i], res);
        }
    }
    
public:
    ThroneInheritance(string kingName) {
        king = new Person(kingName);
        m[kingName] = king;
    }
    
    void birth(string parentName, string childName) {
        Person* child = new Person(childName);
        m[childName] = child;
        m[parentName]->children.push_back(child);
    }
    
    void death(string name) {
        m[name]->alive = false;
    }
    
    vector<string> getInheritanceOrder() {
        vector<string> res;
        dfs(king, res);
        return res;
    }
};
```

