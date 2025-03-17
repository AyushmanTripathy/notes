# Multi-Threading

## Types 

- implmenting the runnable interface

```
class A implements Runnable {
    public void run() {...}
}
Thread t = new Thread(new A());
t.start();
```

- extending the thread class

```
class A extends Thread {
    public void run() {...}
}
A t = new A();
t.start();
```

- `t.run()` would run the code without starting a new thread
- Exception in one thread, doesnot effect others

## Thread class

- `thread.join()`, wait for this thread to die
