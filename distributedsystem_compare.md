# EQs 4. Comparison with state-of-the-art distributed-system-based graph engines  
Finally, we compare `RealGraph+` on the PC system with four distributed-system based graph engines: `PowerGraph`[^Gon12], `GraphLab`[^Low12], `GraphX`[^Gon14], and `Giraph`[^Ave11].
We quote their results for comparison since it is not feasible to construct the identical distributed systems with them.
Note that we use WCC and PR as graph algorithms for comparison since they are the only graph algorithms whose performances on the four distributed-system based graph engines are commonly reported[^Gon12][^Gon14]) for the Twitter dataset.
Table 5 presents the performance of each graph engine and its system environment where Machine indicates the number and type of machines; for each machine, #Cores, Mem.Size, and Storage indicate the number of cores, the size of memory, and the type of storage, respectively.
The hyphen (-) means that no result is available in the respective papers.
We note that the distributed-system-based graph engines use hundreds of cores within dozens of machines, which have much more computing power than our single machine employed by our `RealGraph+`.
Nevertheless, the result shows that `RealGraph+` performs better than distributed-system based engines, even better than `PowerGraph`, the best performer among them.  

 In summary, we conclude RealGraph+ achieves significantly better performance than RealGraph as well as other existing graph engines by increasing its IO-BW on high-performance storage such as NVMe SSD, using much smaller computing resources in a single machine.


<p align="center">
  <img src="https://user-images.githubusercontent.com/39540545/216488745-6564cca6-0f55-448f-93ad-596af0317219.png" />
</p>


[^Gon12]: Powergraph: Distributed graph-parallel computation on natural graphs, Joseph E Gonzalez et al, USENIX OSDI 2012
[^Low12]: Distributed GraphLab: A Framework for Machine Learning and Data Mining in the Cloud, Yucheng Low et al, In VLDB Endowment, 2012
[^Gon14]: Graphx: Graph processing in a distributed dataflow framework, Joseph E Gonzalez et al, USENIX OSDI, 2014
[^Ave11]: Giraph: Large-scale graph processing infrastructure on hadoop, Ching Avery, Proceedings of the Hadoop Summit. Santa Clara, 2011
