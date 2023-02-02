# RealGraphPlus
## EXPERIMENTS
**<u>!!!!!!!!!!! {\m} 을 RealGraph+ 로 변경, {\real} RealGraph !!!!!</u>**  
In this section, we validate the effectiveness of {\m} by answering the following evaluation questions (EQs):  
 - EQ1: Are our optimization strategies effective in improving the performance of {\m}?  
 - EQ2: How much does {\m} improve the original {\real} in terms of the IO-BW/exec. time in graph processing?  
 - EQ3: Does {\m} provide the performance better than state-of-the-art single-machine-based graph engines?  
 - EQ4: Does {\m} provide the performance better than state-of-the-art distributed-system-based graph engines?  
  
  
```ㅁㄴㅇㄹ```  
  
 **Experimental setup.** We run our experiments on two types of single-machine systems of different specifications (Table 3).
We use six real-world datasets [^Jo19] (Table 4 – Wiki, UK, Twitter, SK, Friend, and Yahoo) and four popular graph algorithms – breadth-first search (BFS)[^Sed11], PageRank (PR)[^Pag99], weakly connected component (WCC)[^Suz03], and random walk and restart (RWR)[^Yil08].
For parameter settings, the following values of parameters are employed, following[^Jo19].
We set the numbers of CPU threads and GPU streams as 4 and 32, respectively, and limit MM/DM as 16GB with 1MB block size for the execution of out-of-core algorithms.

<p align="center">
  <img src="https://user-images.githubusercontent.com/47405729/216283494-91898018-cbe2-4142-979d-32022b3a3f61.png" />
</p>


<p align="center">
  <img src="https://user-images.githubusercontent.com/47405729/216283496-0bd65daf-9a13-4593-971f-c1539608e7b5.png" />
</p>

 **EQs 1 and 2. Ablation study.** We (1) verify the effectiveness of our optimization strategies employed in {\m}:  U-IO and A-IO together (UA), and SIMD processing for CPU/GPU (SIMD-C/SIMD-G) and (2) show the superiority of {\m} over the original {\real} (ORG) in terms of the IO-BW/execution time.
We performed graph algorithms on the R750 system whose NVMe SSD provides two times more IO-BW than the PC system, and measured the IO-BW and execution times.
Figure 9 shows the result, where the acronyms separated by a slash (/) in the name indicate corresponding optimization strategies stated above.
We note that the SIMD processing for CPU is applied to all graph algorithms except for BFS, since it does not perform any arithmetic (i.e., PR and RWR) or comparison (i.e., WCC) operations but atomic bit-wise operations which should be executed sequentially.
For example, SIMD-G/UA indicates {\real} with SIMD processing for GPU (SIMD-G) and the U-IO \& A-IO together (UA).
U-IO and A-IO together (UA) improves the performance about 2.1×/1.7× in terms of the IO-BW/execution time, respectively, by reducing the times for **Idle** and **Issue**.
Through A-IO, a thread does not need to wait for the completion of IO in an idle state; through U-IO, a thread becomes free from the context switching overhead between a user mode and a kernel mode. As a result, {\m} succeeded in increasing its IO-BW in storage by issuing IO requests more frequently.
SIMD processing (SIMD-C/SIMD-G) improves the performance about 1.2×/1.4× in CPU and 4.0×/6.2× in GPU, , in terms of the IO-BW/execution time respectively, by reducing the time for **Process**.
Through SIMD processing, a thread parallelizes independent operations of a graph algorithm for a large number of nodes and edges. As a result, {\m} can increase its IO-BW in storage by issuing IO requests more frequently, which leads to the overall performance improvement in graph processing.
SIMD-G requires additional MM-to-DM IO, compared with SIMD-C. However, it performs much faster than SIMC-C because it employs a large number of GPU cores.
In summary, the result indicates that all of our optimization strategies address technical issues explained in Section 3 successfully, thereby increasing the IO-BW and reducing execution times effectively.
Finally, we observe {\real} with the best combination of our strategies (SIMD-G/UA) enhances the performance of {\real} (i.e., ORG) by 5.7×/7.4× (WCC on the Friend dataset), in terms of the IO-BW/execution time, respectively.
We use (SIMD-G/UA) as our best choice for {\m} in the following experiments.

<p align="center">
  <img src="https://user-images.githubusercontent.com/47405729/216280483-39729b29-e936-4732-9c7d-422e63c70144.png" />
</p>


 **EQs 3. Comparison with state-of-the-art single-machine-based graph engines**
We compare {\m} with five single-machine-based graph engines: GraphChi[^Kyr12], X-Stream[^Roy13], TurboGraph[^Han13], GridGraph[^Zhu15], and FlashGraph[^Zhe15].
We run BFS, PR, and WCC, which are commonly provided by all graph engines, by executing each graph engine with 8 CPU threads on each of the PC system with the same specifications, since they require different operating systems (i.e., Windows OS for TurboGraph and Linux OS for the other graph engines).
Figure 7 shows the result where "O.O.M" and "O.O.T" denote the out-of-memory and out-of-time indicating the case exceeding 24 hours, respectively.
We note that TurboGraph does not perform WCC on the Wiki and UK datasets (i.e., infeasible).
We observe that {\m} provides the performance much better than the existing graph engines, especially, by up to 69× better than TurboGraph, the best performer among existing graph engines.



<p align="center">
  <img src="https://user-images.githubusercontent.com/47405729/216280476-c19a88a4-20c9-4c44-8f8b-348b9c48e05f.png" />
</p>



<!-- ![Specifications of our single-machine systems](https://user-images.githubusercontent.com/47405729/216283494-91898018-cbe2-4142-979d-32022b3a3f61.png)

![Statistics of real-world-datasets](https://user-images.githubusercontent.com/47405729/216283496-0bd65daf-9a13-4593-971f-c1539608e7b5.png)


![Effectiveness of optimization strategies](https://user-images.githubusercontent.com/47405729/216280483-39729b29-e936-4732-9c7d-422e63c70144.png)


![Comparison with single-machine-based graph engines](https://user-images.githubusercontent.com/47405729/216280476-c19a88a4-20c9-4c44-8f8b-348b9c48e05f.png) -->


[^Jo19]: RealGraph
[^Sed11]: a
