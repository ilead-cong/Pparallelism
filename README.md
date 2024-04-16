# Pparallelism
python parallelism

python并行执行任务

## python 执行shell

```python

import subprocess as subp

def Subp_call(cmd):
    print(cmd)
    subp.check_call(cmd, shell=True)
    return

```


## python 异步进程池

```python

from multiprocessing import Pool
import time

n_threads = 5

params_list = [[], []]

def Work(i):
    time.spleep(2)
    return

def Multi_process(function, params_list, n_threads):

    pool = Pool(n_threads)
    for param in params_list:
        pool.apply_async(func=function, args=param)
    pool.close()
    pool.join()

    return

```




## python 异步进程池，并获取返回结果

```python

from multiprocessing import Pool
import time

n_threads = 5

params_list = [[], []]

def Work(i):
    time.spleep(2)
    return i

def Multi_process_get(function, params_list, n_threads):

    res_list = []
    pool = Pool(n_threads)
    for param in params_list:
        res = pool.apply_async(func=function, args=param)
        res_list.append(res)
    pool.close()
    pool.join()

    out_list = []
    for res in res_list:
        out_list.append(res.get())
    
    return out_list

```




## python 异步进程池，并同时打印进程进度

```python

from multiprocessing import Pool
import time
from tqdm import tqdm

n_threads = 5

params_list = [[], []]

def Work(i):
    time.spleep(2)
    return i

def Multi_process(function, params_list, n_threads, description=""):
    
    pbar = tqdm(total=len(params_list))
    pbar.set_description(description)
    update = lambda *args: pbar.update()

    pool = Pool(n_threads)
    for param in params_list:
        pool.apply_async(function, param, callback=update)
    pool.close()
    pool.join()

    return

```



## python 异步进程池，获取返回结果, 并同时打印进程进度

```python

from multiprocessing import Pool
import time
from tqdm import tqdm

n_threads = 5

params_list = [[], []]

def Work(i):
    time.spleep(2)
    return i

def Multi_process(function, params_list, n_threads, description=""):
    
    pbar = tqdm(total=len(params_list))
    pbar.set_description(description)
    update = lambda *args: pbar.update()


    res_list = []
    pool = Pool(n_threads)
    for param in params_list:
        res = pool.apply_async(func=function, args=param, callback=update)
        res_list.append(res)
    pool.close()
    pool.join()

    out_list = []
    for res in res_list:
        out_list.append(res.get())

    return out_list


```
