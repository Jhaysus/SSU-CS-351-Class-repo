Project 2

![Mean speedup graph](means.png)


Does it “converge” to some general value? What’s the maximum speedup you got from threading? What happens when you use more cores than are available in the hardware?
The graph converges at around the 38 thread, where it stays at around 18. It continues this thread as it longer speeds up. The speedup curve initially increases rapidly as additional threads are introduced, but it eventually converges to a nearly constant value. In this experiment, the speedup converges at around 38 threads, where it stabilizes at approximately 18×. Beyond this point, adding more threads does not result in further performance improvement.

This behavior occurs because the number of threads exceeds the number of available hardware cores. Once all cores are fully utilized, additional threads introduce scheduling overhead and contention for shared resources such as memory bandwidth, preventing further speedup and, in some cases, slightly degrading performance.

Considering the number of cores in the system, do you get a linear scaling of performance as you add more cores?


The performance does not demonstrate a scale linearly. Initial speedup is close to linear, but diminishing returns appear as thread count approaches the number of hardware cores due to serial overhead and shared resource contention.

what value would you proposed for p, and describe how you arrived at that value.

Based on the speedup graph, performance converges at a maximum speedup of approximately 18×. Using Amdahl’s Law, this corresponds to a parallelizable fraction of p ≈ 0.94, meaning about 94% of the program can be parallelized. The remaining ~6% of serial work limits further speedup as additional threads are added.

Each iteration of the mean kernel reads one double, requiring 8 bytes per iteration. Based on the total data size and runtime, the kernel achieves higher effective bandwidth with threading, but the bandwidth increase eventually plateaus as memory limits are reached. This behavior is consistent across threaded versions, indicating the computation is memory-bandwidth bound rather than compute-bound.

![Mean speedup graph](sdf.png)


The performance curve for the SDF computation is similar in shape to the mean computation in that speedup increases as more threads are added. However, unlike the mean computation, the SDF speedup appears closer to linear over the tested range. This is because the SDF kernel performs more computation per iteration and is less constrained by memory bandwidth, allowing it to scale more efficiently with additional threads.
