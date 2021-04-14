https://leetcode.com/problems/the-dining-philosophers/

```c++
// c++
class DiningPhilosophers {
private:
    int n;
    vector<mutex> locks;
    inline int leftFork (int id) { return id; }
    inline int rightFork (int id) { return (id + 1) % 5; }
public:
    DiningPhilosophers()   {
        n = 5;
        locks = vector<mutex>(n);
    }
    void wantsToEat(int philosopher,
                    function<void()> pickLeftFork,
                    function<void()> pickRightFork,
                    function<void()> eat,
                    function<void()> putLeftFork,
                    function<void()> putRightFork) {
        if (philosopher == 0) {
            locks[rightFork(philosopher)].lock(); 
            locks[leftFork(philosopher)].lock(); 
            pickLeftFork();
            pickRightFork();
            eat();
            putLeftFork();
            putRightFork();
            locks[rightFork(philosopher)].unlock(); 
            locks[leftFork(philosopher)].unlock();
        } else {
            locks[leftFork(philosopher)].lock();
            locks[rightFork(philosopher)].lock(); 
            pickLeftFork();
            pickRightFork();
            eat();
            putLeftFork();
            putRightFork();
            locks[leftFork(philosopher)].unlock(); 
            locks[rightFork(philosopher)].unlock();
        }
    }
};
```



```java
class DiningPhilosophers {
    private int n;
    private ReentrantLock[] locks;
    public DiningPhilosophers() {
        n = 5;
        locks = new ReentrantLock[n];
        for (int i = 0; i < n; i++) locks[i] = new ReentrantLock();
    }
    // call the run() method of any runnable to execute its code
    public void wantsToEat(int philosopher,
                           Runnable pickLeftFork,
                           Runnable pickRightFork,
                           Runnable eat,
                           Runnable putLeftFork,
                           Runnable putRightFork) throws InterruptedException {
        int leftFork = philosopher;
        int rightFork = (philosopher + 1) % n;
        
        if (philosopher == 0) {
            locks[rightFork].lock();
            locks[leftFork].lock();
            pickLeftFork.run();
            pickRightFork.run();
            eat.run();
            putLeftFork.run();
            putRightFork.run();
            locks[rightFork].unlock();
            locks[leftFork].unlock();
        } else {
            locks[leftFork].lock();
            locks[rightFork].lock();
            pickLeftFork.run();
            pickRightFork.run();
            eat.run();
            putLeftFork.run();
            putRightFork.run();
            locks[leftFork].unlock();
            locks[rightFork].unlock();
        }
    }
}
```

