# ELT(数据仓库)

### 1.基本定义

**ELT**（Extract-Load-Transform）是利用数据库的处理能力的技术。



**ETL**，是英文Extract-Transform-Load的缩写，用来描述将[数据](https://baike.baidu.com/item/数据/5947370)从来源端经过抽取（extract）、[转换](https://baike.baidu.com/item/转换/197560)（transform）、加载（load）至目的端的过程。**ETL**一词较常用在[数据仓库](https://baike.baidu.com/item/数据仓库)，但其对象并不限于数据仓库。

ETL是将业务系统的数据经过抽取、清洗转换之后加载到数据仓库的过程，目的是将企业中的分散、零乱、标准不统一的数据整合到一起，为企业的决策提供分析依据， ETL是BI（[商业智能](https://baike.baidu.com/item/商业智能/406141)）项目重要的一个环节。

**ETL**所描述的过程，一般常见的作法包含**ETL**或是**[ELT](https://baike.baidu.com/item/ELT/9352740)**（Extract-Load-Transform），并且混合使用。通常越大量的数据、复杂的转换逻辑、目的端为较强运算能力的[数据库](https://baike.baidu.com/item/数据库)，越偏向使用**ELT**，以便运用目的端[数据库](https://baike.baidu.com/item/数据库)的平行处理能力。



ELT是利用数据库的处理能力，E=从源数据库抽取数据，L=把数据加载到目标库的临时表中，T=对临时表中的数据进行转换，然后加载到目标库目标表中。

### 2.ELT优点

1. ELT主要通过数据库引擎来实现系统的可扩展性（尤其是当数据加工过程在晚上时，可以充分利用数据库引擎的资源）

2. ELT可以保持所有的数据始终在数据库当中，避免数据的加载和导出，从而保证效率，提高系统的可监控性。

3. ELT可以根据数据的分布情况进行并行处理优化，并可以利用数据库的固有功能优化磁盘I/O。

4. ELT的可扩展性取决于数据库引擎和其硬件服务器的可扩展性。

5. 通过对相关数据库进行性能调优，ETL过程获得3到4倍的效率提升一般不是特别困难。

### 3.ELT工具

和基于ETL架构的工具（[Kettle](https://baike.baidu.com/item/Kettle)、[Talend](https://baike.baidu.com/item/Talend)、[Datastage](https://baike.baidu.com/item/Datastage)、[Informatica](https://baike.baidu.com/item/Informatica)）相比，基于ELT架构的工具目前并不多（OWB、HaoheDI）