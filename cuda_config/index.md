# 环境配置-cuda


cuda和cudnn的安装

<!--more-->

## 1 本人配置

以下是本人电脑配置:

* 系统：Windows10
* CPU：AMD Ryzen 7 4800H
* 显卡：GTX2060

## 2 安装cuda和cudnn

### 2.1 安装cuda

{{< admonition abstract >}}
CUDA(Compute Unified Device Architecture)，具体详细解释可以网上去查。总之CUDA就是一个并行计算架构，可以提升你GPU处理复杂计算的能力，也就是加速你程序运行速度。因为图像处理主要就是矩阵运算，所以为了提高计算速度可以安装CUDA。而NVIDIA的GPU显卡驱动程序和CUDA是两个完全不同的概念。你只需要知道CUDA就是一个运行在GPU上的ToolKit即可。总之你电脑虽然安装了显卡驱动，但还是要安装CUDA。
首先需查看当前显卡驱动程序版本。这里由于每个电脑打开此界面的方法可能不同，需要自己到网上去查怎么查看显卡驱动程序版本。
{{< /admonition >}}
第一步，查看显卡驱动程序版本，如下图Fig. 1.所示。
{{< image src="2_1.png" caption="Fig. 1. 显卡驱动程序版本" width="640" height="320" >}}
第二步，再到[NVIDIA官网](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html)查看显卡信息对照CUDA Toolkit and Compatible Versions表。由于我们的显卡驱动程序版本是 471.11，所以这里选择CUDA 11.4.0及以下版本即可。如图Fig. 2.所示。
{{< image src="2_2.png" caption="Fig. 2. CUDA Toolkit and Compatible Versions表" width="640" height="320" >}}
第四步，下载下来，一路确定即可。
第三步，再到[此网址](https://developer.nvidia.com/cuda-toolkit-archive)选择CUDA 11.4.0及以下版本进行下载（由于之前我安装过一次，选择的是CUDA 11.1版本），如下图Fig. 3.所示。
{{< image src="2_3.png" caption="Fig. 3. CUDA 11.1" width="640" height="320" >}}
{{< admonition >}}
由于这个小版本号可能过一段时间会更新，因为我以前安装的时候是11.1.7_455.06版本，但不用担心，只要大版本号（比如这里的11.1）一致就行。
{{< /admonition >}}
第四步，下载下来，一路确定即可。

### 2.2 安装cudnn

第一步，到[此界面](https://developer.nvidia.com/rdp/cudnn-archive)下载与cudn大版本号对应的版本，如下图Fig. 4.所示。
{{< image src="2_4.png" caption="Fig. 4. CUDNN 8.1.1" width="640" height="320" >}}
{{< admonition >}}
需要说的是，这里图Fig. 5.虽然显示的是windows x86，但下载下来的是x64。所以不用担心，直接下载即可。
{{< image src="2_5.png" caption="Fig. 5. windows x86" width="640" height="320" >}}
{{< /admonition >}}
第二步，把下载下来的包解压之后，将里面的bin、include、lib文件直接复制到CUDA的安装目录下，直接覆盖即可。如下图Fig. 6.所示
{{< image src="2_6.png" caption="Fig. 6. CUDA安装目录" width="640" height="320" >}}

## 3 验证

打开命令行输入nvcc -V，显示类似如下图Fig. 7.结果就行
{{< image src="2_7.png" caption="Fig. 7. nvcc" width="640" height="320" >}}

