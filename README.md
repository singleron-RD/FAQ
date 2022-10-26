# FAQ

- C2较C3算法比较，C3会增加一定比例的细胞数量，增加的细胞数与C2相比差距较大，增加的细胞是什么细胞？C2与C3算法该如何选择？

https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/algorithms/overview#cell_calling

增加的细胞理论上为低表达的细胞，通常情况下大多数为免疫细胞，可以通过细胞类型注释查看。异质性高的样本建议使用C3（EmptyDrops_CR）算法，例如肿瘤样本。

- C3算法是否依赖barcode UMI rank曲线？	

C3算法不依赖于曲线。

- C3算法分析后出现细胞数量大于投入的细胞总量时，如何解释？多出的细胞该怎么处理？	

实验方面，投入细胞数计数也许不准，例如有损伤细胞时，可能造成捕获的细胞数比实际投入的多。  如果不需要这么多细胞，可以强制细胞数或者通过下游过滤去除。
具体可参考https://support.bioconductor.org/p/118877/。

- 分析报告中的关键质控指标有哪些，如何从这些关键指标中判断数据优劣？

以下指标越高越好，低于阈值说明样本质量有问题。
```
Valid Reads: > 85%
Uniquely mapped Reads: > 65%
Reads Assigned: > 70%
Fraction of Reads in Cells: > 50%
```

- 跑celescope流程时，哪些参数的设置可能影响指标？

celescope版本 < 1.12.0, 建议设置以下参数:

1. `--gtf_type gene`, 可以将mapping到intron的reads计入，以提高Median genes
2. 加入参数`--allowNoPolyT`, 可以提高Valid Reads


celescope版本 >= 1.12.0版本:

使用`celescope utils mkgtf`过滤gtf中的基因，可以降低线粒体基因含量。过滤后的gtf也可以用于celescope版本 < 1.12.0



- 下游分析时如何质控细胞质量进行细胞筛选。
线粒体过滤阈值？

- 生信分析其他注意事项和分析经验介绍（举例介绍）