###### ITT 440 INDIVIDUAL LABWORK
---
# Task: Calculate Factorial Number By Using Parallel Programming 
---
## What is Parallel Programming? 
Parallel computing is a type of computation in which many calculations or processes are carried out simultaneously. 
This is in contrast to sequential computing, where calculations are performed one after the other. 
In parallel computing, tasks are broken down into smaller parts that can be executed concurrently, 
either on multiple processors within a single computer or across a network of interconnected computers.

### Scope of Parallel Computing
1. Applications in engineering and design.
   - eg: Airfoils, internal combustion engines, high speed circuit etc.
2. Scientific applications.
   - eg: Sequencing of human genome, analyze biological sequence etc.
3. Commercial applications.
   - eg: Wall street – large scale transactions, data mining and analysis etc.
4. Application in computer systems.
   - eg: Computer security, embedded systems, etc

Note:
  - Parallel programming helps developers break down the tasks 
that a program must be completed into smaller segments of work 
that can be done in parallel.
  - While parallel programming can be a more time-intensive 
effort up front for developers to create efficient parallel 
algorithms and code, it overall saves time by leveraging 
parallel processing power by running the program across 
multiple compute nodes and CPU cores at the same time.

## Let's Start The Code (using Phyton Programming Language) :satisfied:
```
import multiprocessing
import math

def factorial(x):
    return math.factorial(x)

if __name__ == '__main__':
    pool = multiprocessing.Pool()
    result_async = [pool.apply_async(factorial, args=(i,)) for i in range(10)]
    results = [r.get() for r in result_async]
    print("Output: {}".format(results))
```

## Expected Output:
```
Output: [1, 1, 2, 6, 24, 120, 720, 5040, 40320, 362880]
```

thank you :blush:


