# To run the experiments, download the zip file containing the code, and a detailed README file will guide you.

# ADDITIONAL Comparison with related work PrivSyn and SLIMView

## Important: All the experiments (presented in the paper and here) are repeated 10 times and we took the average result 

**PrivSyn: Differentially Private Data Synthesis**
**Authors: Zhikun Zhang, Tianhao Wang, Ninghui Li, Jean Honorio, Michael Backes, Shibo He1, Jiming Chen, Yang Zhang**
**In 30th USENIX Security Symposium (USENIX Security 21) (pp. 929-946)**


In this experiment, we compared \texttt{RIPOST} with another generative method, PrivSyn, which improves upon the work done in PrivBayes. PrivSyn has high computational complexity, making it infeasible to scale to all tests conducted in the main experiments of this paper. To compare it with \texttt{RIPOST}, we performed experiments on a set of tensors with dimensions ranging from 2D to 6D using the Adult dataset, each with its own workload of 100 queries.

![alt text](https://github.com/AlaEddineLaouir/RIPOST/blob/main/edbt-privsyn-adult.jpg?raw=true)

From the above figure, we observe that PrivSyn exhibits performance similar to PrivBayes. This is because these generative solutions do not take into account the \textit{Measure} attribute and are primarily optimized for tabular data rather than multidimensional tensors. Additionally, we notice that PrivSyn's performance improves as the number of dimensions increases. This is due to fewer splits being performed, which causes the values in the \textit{Measure} attribute to become smaller and closer to 0/1, reducing its impact.

In conclusion, similar to PrivBayes, PrivSyn is not able to outperform \texttt{RIPOST} in OLAP tasks involving tensors and range queries.

**Ala Eddine Laouir and Abdessamad Imine. 2024. SLIM-View: Sampling and**
**Private Publishing of Multidimensional Databases. In Proceedings of the Fourteenth**
**ACM Conference on Data and Application Security and Privacy. 391–402.**


In this experiment, we examine the performance of \texttt{RIPOST} compared to SLIMView. Note that SLIMView is somewhat a hybrid system that perturbs the data to create a view but cannot publish it directly, as the noise is added online during query execution. Thus, SLIMView is limited in this sense, making it different from the true data publishing approach performed by \texttt{RIPOST}.

SLIMView can operate with or without a predefined workload. We refer to the version with a workload as \texttt{SLIMView}, and the version without a workload as \texttt{SLIMView-WW}. We conducted experiments using the Adult dataset, generating tensors and workloads with dimensions ranging from 2D to 6D—the same ones used in our main experiments. The comparative results are shown in the following Figure.

![alt text](https://github.com/AlaEddineLaouir/RIPOST/blob/main/edbt-slim-adult.jpg?raw=true)

We observe that \texttt{RIPOST} outperforms both \texttt{SLIMView} and \texttt{SLIMView-WW} in the tests conducted on 2D, 3D, and 4D tensors. However, it falls behind in the 5D and 6D tests. This is due to the higher number of dimensions resulting in less aggregation, which causes the values in the cells to become smaller. Since \texttt{SLIMView} (and \texttt{SLIMView-WW}) uses sampling on non-empty cells, the error from sampling decreases as the values in these cells get smaller.

To verify this observation, we took one 6D tensor and randomly added values (ranging from 0 to 200) to its non-empty cells. We then conducted a test with 3,000 queries. In Figure~\ref{fig:synth6}, we observe the results of this test labeled as \texttt{Synth-6} on the x-axis. It shows that in this case, even for higher-dimensional tensors, \texttt{RIPOST} outperforms \texttt{SLIMView}.


