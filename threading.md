# Threading in python

### Example 1
```python
from threading import Thread
import time

def timer(name, delay, repeat):
    print "Timer: " + name + " Started"
    while repeat > 0:
        time.sleep(delay)
        print name + ": " + str(time.ctime(time.time()))
        repeat -= 1
    print "Timer: " + name + " Completed"

def Main():
    t1 = Thread(target=timer, args=("Timer1", 1, 5))
    t2 = Thread(target=timer, args=("Timer2", 2, 5))
    t1.start()
    t2.start()
    
    print "Main complete"

if __name__ == '__main__':
    Main()
```

### Example 2
```python
import threading
import time

class AsyncWrite(threading.Thread):
    def __init__(self, text, out):
        threading.Thread.__init__(self)
        self.text = text
        self.out = out

    def run(self):
        f = open(self.out, "a")
        f.write(self.text + '\n')
        f.close()
        time.sleep(2)
        print "Finished Background file write to " + self.out
        

def Main():
    message = raw_input("Enter a string to store:" )
    background = AsyncWrite(message, 'out.txt')
    background.start()
    print "The program can continue while it writes in another thread"
    print "100 + 400 = ", 100+400

    background.join()
    print "Waited until thread was complete"

if __name__ == '__main__':
    Main()
```

### Example 3

Only one timer can use the lock at a given time in this example.\
Use semaphores if you want 10 threads running but you only want 2 or 3 to have access to a piece of data at a time.
```python
import threading
import time

tLock = threading.Lock()

def timer(name, delay, repeat):
    print "Timer: " + name + " Started"
    tLock.acquire()
    print name + " Has Acquired the lock"
    while repeat > 0:
        time.sleep(delay)
        print name + ": " + str(time.ctime(time.time()))
        repeat -= 1
    print name + " is releasing the lock"
    tLock.release()
    print "Timer: " + name + " Completed"

def Main():
    t1 = threading.Thread(target=timer, args=("Timer1", 1, 5))
    t2 = threading.Thread(target=timer, args=("Timer2", 2, 5))
    t1.start()
    t2.start()
    
    print "Main complete"

if __name__ == '__main__':
    Main()
    
```