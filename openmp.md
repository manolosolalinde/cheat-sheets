# Tutorial OpenMP - Parallel programming

https://www.youtube.com/watch?v=jdYHVeh2wEI&list=PLLX-Q6B8xqZ8n8bwjGdzBJ25X2utwnoEG&index=10

https://www.openmp.org/wp-content/uploads/Intro_To_OpenMP_Mattson.pdf

Directivas \
https://www.openmp.org/wp-content/uploads/OpenMP-4.5-1115-CPP-web.pdf

## Keywords

```cpp
omp_get_thread_num() //Gets current thread
omp_set_num_threads(NUM_THREADS) //Request and set number of threads (less may be granted)
omp_get_num_threads() // Get number of threads

#pragma omp parallel
#pragma omp critical // Allow only one thread to access this part of the code at once
#pragma omp barrier // Wait for every thread to finish previous task before starting

#pragma omp for // Note: there is a barrier to start the loop by default
#pragma omp for nowait //nowait removes the barrier to start the loop inmediately
#pragma omp for reduction(+:sum) // Crea una variable local 'sum' en cada proceso y luego las adiciona
#pragma omp parallel for 

#pragma omp master //only id 0 will run this
#pragma omp single //the first that gets there does it. Note: there is a barrier at the end.
//example
#pragma omp parallel
{
    do_many_things();
    #pragma omp single
        { exchange_boundaries(); }
    do_many_other_things();
}

//to control how loops are distributed
omp_get_schedule()
omp_set_schedule(option) //option can be static, dynamic, etc.
```

## Examples


Unelegant integral problem solution (false sharing solved)
```cpp
#include <omp.h>
static long num_steps = 100000; double step;
#define PAD 8 // assume 64 byte L1 cache line size
#define NUM_THREADS 2
void main ()
{
    int i, nthreads; double pi, sum[NUM_THREADS][PAD];
    step = 1.0/(double) num_steps;
    omp_set_num_threads(NUM_THREADS);
    #pragma omp parallel
    {
        int i, id,nthrds;
        double x;
        id = omp_get_thread_num();
        nthrds = omp_get_num_threads();
        if (id == 0) nthreads = nthrds;
        for (i=id, sum[id]=0.0;i< num_steps; i=i+nthrds) {
            x = (i+0.5)*step;
            sum[id][0] += 4.0/(1.0+x*x);
        }
    }
    for(i=0, pi=0.0;i<nthreads;i++)pi += sum[i][0] * step;
}
```

Elegant integral problem solution
```C
#include <omp.h>
static long num_steps = 100000; double step;
#define NUM_THREADS 2
void main ()
{
    double pi; step = 1.0/(double) num_steps;
    omp_set_num_threads(NUM_THREADS);
    #pragma omp parallel
    {
        int i, id,nthrds; double x, sum;
        id = omp_get_thread_num();
        nthrds = omp_get_num_threads();
        if (id == 0) nthreads = nthrds;
        id = omp_get_thread_num();
        nthrds = omp_get_num_threads();
        for (i=id, sum=0.0;i< num_steps; i=i+nthreads){
            x = (i+0.5)*step;
            sum += 4.0/(1.0+x*x);
        }
        //critical case
        #pragma omp critical
        pi += sum * step;

        // // atomic case
        // sum = sum*step;
        // #pragma atomic
        // pi +=sum;
    }
}
```

Using a loop and a reduction
```cpp
#include <omp.h>
static long num_steps = 100000; double step;
void main ()
{ 
    int i; double x, pi, sum = 0.0;
    step = 1.0/(double) num_steps;
    #pragma omp parallel
    {
        double x; //Create a scalar local to each thread to hold value of x at the center of each interval
        #pragma omp for reduction(+:sum)
        for (i=0;i< num_steps; i++){
            x = (i+0.5)*step;
            sum = sum + 4.0/(1.0+x*x);
        }
    }
    pi = step * sum;
}
```

