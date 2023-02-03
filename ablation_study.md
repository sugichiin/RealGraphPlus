# EQs 1 and 2. Ablation study.
We (1) verify the effectiveness of our optimization strategies employed in RealGraph+:  U-IO and A-IO together `(UA)`, and SIMD processing for CPU/GPU `(SIMD-C/SIMD-G)` and (2) show the superiority of RealGraph+ over the original RealGraph `(ORG)` in terms of the IO-BW/execution time.
We performed graph algorithms on the R750 system whose NVMe SSD provides two times more IO-BW than the PC system, and measured the IO-BW and execution times.
Figure 6 shows the result, where the acronyms separated by a slash (/) in the name indicate corresponding optimization strategies stated above.
We note that the SIMD processing for CPU is applied to all graph algorithms except for BFS, since it does not perform any arithmetic (i.e., PR and RWR) or comparison (i.e., WCC) operations but atomic bit-wise operations which should be executed sequentially.
For example, `SIMD-G/UA` indicates RealGraph with SIMD processing for GPU `(SIMD-G)` and the U-IO \& A-IO together `(UA)`.
U-IO and A-IO together `(UA)` improves the performance about 2.1×/1.7× in terms of the IO-BW/execution time, respectively, by reducing the times for **Idle** and **Issue**.
Through A-IO, a thread does not need to wait for the completion of IO in an idle state; through U-IO, a thread becomes free from the context switching overhead between a user mode and a kernel mode. As a result, RealGraph+ succeeded in increasing its IO-BW in storage by issuing IO requests more frequently.
SIMD processing `(SIMD-C/SIMD-G)` improves the performance about 1.2×/1.4× in CPU and 4.0×/6.2× in GPU, in terms of the IO-BW/execution time respectively, by reducing the time for **Process**.
Through SIMD processing, a thread parallelizes independent operations of a graph algorithm for a large number of nodes and edges. As a result, RealGraph+ can increase its IO-BW in storage by issuing IO requests more frequently, which leads to the overall performance improvement in graph processing.
`SIMD-G` requires additional MM-to-DM IO, compared with `SIMD-C`. However, it performs much faster than `SIMD-C` because it employs a large number of GPU cores.
In summary, the result indicates that all of our optimization strategies address technical issues explained in Section 3 successfully, thereby increasing the IO-BW and reducing execution times effectively.
Finally, we observe RealGraph with the best combination of our strategies `(SIMD-G/UA)` enhances the performance of RealGraph (i.e., `ORG`) by 5.7×/7.4× (WCC on the Friend dataset), in terms of the IO-BW/execution time, respectively.
We use `(SIMD-G/UA)` as our best choice for RealGraph+ in the following experiments.

<p align="center">
  <img src="https://user-images.githubusercontent.com/47405729/216280483-39729b29-e936-4732-9c7d-422e63c70144.png" />
</p>
