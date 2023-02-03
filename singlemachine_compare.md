# EQs 3. Comparison with state-of-the-art single-machine-based graph engines  
We compare `RealGraph+` with five single-machine-based graph engines: `GraphChi`[^Kyr12], `X-Stream`[^Roy13], `TurboGraph`[^Han13], `GridGraph`[^Zhu15], and `FlashGraph`[^Zhe15].
We run BFS, PR, and WCC, which are commonly provided by all graph engines, by executing each graph engine with 8 CPU threads on each of the PC system with the same specifications, since they require different operating systems (i.e., Windows OS for `TurboGraph` and Linux OS for the other graph engines).
Figure 7 shows the result where "O.O.M" and "O.O.T" denote the out-of-memory and out-of-time indicating the case exceeding 24 hours, respectively.
We note that `TurboGraph` does not perform WCC on the Wiki and UK datasets (i.e., infeasible).
We observe that `RealGraph+` provides the performance much better than the existing graph engines, especially, by up to 69× better than `TurboGraph`, the best performer among existing graph engines.



<p align="center">
  <img src="https://user-images.githubusercontent.com/47405729/216280476-c19a88a4-20c9-4c44-8f8b-348b9c48e05f.png" />
</p>

[^Kyr12]: GraphChi: Large-scale graph computation on just a pc, Aapo Kyrola et al, USENIX OSDI, 2012
[^Roy13]: X-Stream: Edge-centric graph processing using streaming partitions, Amitabha Roy et al, ACM SOSP, 2013
[^Han13]: TurboGraph: A fast parallel graph engine handling billion-scale graphs in a single PC, Wook-Shin Han et al, ACM KDD, 2013
[^Zhu15]: Gridgraph: Large-scale graph processing on a single machine using 2-level hierarchical partitioning, Xiaowei Zhu et al, USENIX ATC, 2015
[^Zhe15]: FlashGraph: Processing billion-node graphs on an array of commodity SSDs, Da Zheng et al, USENIX FAST, 2015
