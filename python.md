
Interact with code

```python
import code
code.interact(local=dict(globals(), **locals()))
```

Check module path

```python
import tensorflow
print(tensorflow.__file__)
import os
path = os.path.dirname(tensorflow.__file__)
```

Testing pandas
```python
import pandas as pd
df = pd.DataFrame([[0.1, 2, 1], [1, 3, 2], [4, 6, 3], [4, 3, 4], [5, 4, 5]], columns=['A', 'B', 'C'])
df.head(2)
```
# Decorators

Useful code extracted from https://github.com/CoreyMSchafer/code_snippets/blob/master/Decorators/decorators.py
Tutorial in: https://www.youtube.com/watch?v=FsAPt_9Bf3U
```python
from functools import wraps

def my_logger(orig_func):
    import logging
    logging.basicConfig(filename='{}.log'.format(orig_func.__name__), level=logging.INFO)
    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        logging.info(
            'Ran with args: {}, and kwargs: {}'.format(args, kwargs))
        return orig_func(*args, **kwargs)
    return wrapper

def my_timer(orig_func):
    import time
    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = orig_func(*args, **kwargs)
        t2 = time.time() - t1
        print('{} ran in: {} sec'.format(orig_func.__name__, t2))
        return result
    return wrapper

import time

@my_logger
@my_timer
def display_info(name, age):
    time.sleep(1)
    print('display_info ran with arguments ({}, {})'.format(name, age))

display_info('Tom', 22)
```



# Links interesantes

Informacion sobre como usar pandas - dataframe \
https://www.ritchieng.com/creating-dataframe-from-objects/