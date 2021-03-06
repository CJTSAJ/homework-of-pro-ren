# xPU
## 1 简介
XPU是百度与Xilinx公司在2017年Hotchips大会上发布的FPGA智能云加速芯片，含256核。
![](https://github.com/CJTSAJ/homework-of-pro-ren/blob/master/Homework2/PPT/XPU1.png)
## 2 基于FPGA的AI和数据分析的工作负载情况
![](https://github.com/CJTSAJ/homework-of-pro-ren/blob/master/Homework2/PPT/XPU3.png)
## 3 XPU框架结构
为了支持矩阵、卷积，以及其他大大小小的内核，我们需要一个配备高带宽低延时内存，以及高带宽I/O接口的大型数学阵列。FPGA中XPU的DSP单元提供了并行处理能力，片外DDR4和HBM接口优化了数据传输，而片上SRAM则提供了必要的存储特性。

![](https://github.com/CJTSAJ/homework-of-pro-ren/blob/master/Homework2/PPT/XPU2.png)
## 4 XPU的特点
### 4.1 优势：
#### 4.1.1 效率、性能和灵活性
XPU架构突出多样性，着重于计算密集型、基于规则的任务，同时确保效率、性能和灵活性的最大化。XPU的目标是在性能和效率之间实现平衡，并处理多样化的计算任务。
#### 4.1.2 多样性
FPGA加速器本身很擅长处理某些计算任务，但随着许多小内核交织在一起，多样性程度将会上升。
### 4.2 缺陷：
欠缺可编程能力，这是基于FPGA框架的通病，这意味着开发者只能使用汇编语言。
### 4.3 Micro Benchmark测试：
在Micro Benchmark测试中，对于计算密集型、常规内存访问的计算任务，XPU的效率与x86内核类似。对于数据同步的计算任务，XPU的可扩展性应当可以进一步优化。而对于没有数据同步的计算任务，XPU的可扩展性与核心数量呈线性关系。
## 5 FPGA
### 5.1 简介：
FPGA（Field－Programmable Gate Array），即现场可编程门阵列，它是在PAL、GAL、CPLD等可编程器件的基础上进一步发展的产物。它是作为专用集成电路（ASIC）领域中的一种半定制电路而出现的，既解决了定制电路的不足，又克服了原有可编程器件门电路数有限的缺点。
### 5.2 工作原理：
FPGA采用了逻辑单元阵列LCA（Logic Cell Array）这样一个概念，内部包括可配置逻辑模块CLB（Configurable Logic Block）、输入输出模块IOB（Input Output Block）和内部连线（Interconnect）三个部分。 现场可编程门阵列（FPGA）是可编程器件，与传统逻辑电路和门阵列（如PAL，GAL及CPLD器件）相比，FPGA具有不同的结构。FPGA利用小型查找表（16×1RAM）来实现组合逻辑，每个查找表连接到一个D触发器的输入端，触发器再来驱动其他逻辑电路或驱动I/O，由此构成了既可实现组合逻辑功能又可实现时序逻辑功能的基本逻辑单元模块，这些模块间利用金属连线互相连接或连接到I/O模块。FPGA的逻辑是通过向内部静态存储单元加载编程数据来实现的，存储在存储器单元中的值决定了逻辑单元的逻辑功能以及各模块之间或模块与I/O间的联接方式，并最终决定了FPGA所能实现的功能，FPGA允许无限次的编程。
## 6 Xilinx
### 6.1 简介：
Xilinx(赛灵思)是全球领先的可编程逻辑完整解决方案的供应商,全球最大的可编程芯片（FPGA）厂商。Xilinx研发、制造并销售范围广泛的高级集成电路、软件设计工具以及作为预定义系统级功能的IP（Intellectual Property）核。
### 6.2 Xilinx FPGA Kintex UltraScale:
XPU基于Xilinx FPGA Kintex UltraScale器件研发。其提供了 ASIC 级系统级性能、时钟管理和功耗管理功能，为下一代器件提升了单位功耗性价比。这些第二代器件为中高容量应用提供最大吞吐量和最低延迟，从而扩展了中端应用，这些应用包括 100G 网络、无线基础设施、和其他 DSP 密集型应用。以 UltraScale 架构 ASIC 级功能为基础的 Kintex UltraScale 器件与 Vivado Design Suite实现了协同优化，并利用 UltraFAST 设计方法 加速产品上市进程。

优势：

1.具有类似于 ASIC 的时钟功能，以实现可扩展性、高性能和更低的动态功耗

2.具有新一代布线方法，以实现快速时序收敛

3.具有改进的逻辑架构，以最大限度地提高性能和器件利用率

## Reference
1. [Xilinx官网](http://china.xilinx.com/)
2. [Baidu details FPGA-based Cloud acceleration with 256-core XPU today at Hot Chips in Cupertino, CA](https://forums.xilinx.com/t5/Xcell-Daily-Blog-Archived/Baidu-details-FPGA-based-Cloud-acceleration-with-256-core-XPU/ba-p/788151)
3. [ Xilinx Kintex UltraScale+ FPGAs](https://www.xilinx.com/products/silicon-devices/fpga/kintex-ultrascale-plus.html)


