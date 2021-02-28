### Collections.sort排序内部原理?

- 在Java 6中Arrays.sort()和Collections.sort()使用的是MergeSort，归并排序
- 而在Java 7中，内部实现换成了TimSort，TimSort算法就是找到已经排好序数据的子序列，然后对剩余部分排序，然后合并起来。


