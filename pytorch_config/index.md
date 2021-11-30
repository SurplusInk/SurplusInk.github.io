# 环境配置-pytorch


Windows下pytorch的GPU环境配置

<!--more-->

## 1 本人配置

以下是本人电脑配置:

* 系统：Windows10
* CPU：AMD Ryzen 7 4800H
* 显卡：GTX2060

{{< admonition >}}
一定要到[NVIDIA官网](https://developer.nvidia.com/cuda-gpus)查看你的显卡是否支持CUDA，如果不支持后面的步骤就不用看了（当然你能找到奇门办法也可以）。
如下图Fig. 1.所示，我的GTX2060显卡支持CUDA且算力为7.5。
{{< image src="1_1.png" caption="Fig. 1. cuda-gpus" width="640" height="320" >}}
{{< /admonition >}}

## 2 安装pytorch-gpu

如果没安装Anaconda，需先安装[Anaconda](https://www.anaconda.com/products/individual)，如果速度过慢可以复制下载链接到迅雷下载，或者使用[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/?C=M&O=D)。

### 2.1 预先准备

打开命令行输入**nvidia-smi**命令查看显卡驱动版本和CUDA版本，如下图Fig. 2.所示。

{{< image src="1_2.png" caption="Fig. 2. nvidia" width="640" height="320" >}}

{{< admonition >}}
这里的CUDA Version只是你目前对应的显卡驱动所支持的最高CUDA版本，意思后面你不能安装比这个版本高的CUDA。
{{< /admonition >}}

### 2.2 创建虚拟环境

由于我后面是安装的pytorch1.8.2版本所以这里虚拟环境取的pytorch1.8，你可以取其它名字。

```conda
conda create -n pytorch1.8 python=3.7  
conda activate pytorch1.8              
```

{{< admonition >}}
目前Windows上pytorch只支持Python 3.x版本，不再支持Python 2.x版本。
{{< /admonition >}}

### 2.3 安装pytorch-gpu

安装pytorch-gpu非常简单，直接到[pytorch官网](https://pytorch.org/get-started/locally/)下载即可。
这里我直接安装的LTS(1.8.2)长期支持版，如下图Fig. 3.所示。

{{< image src="1_3.png" caption="Fig. 3. pytorch-1.8.2" width="640" height="320" >}}

即输入以下命令。

```pip
conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch-lts -c conda-forge
```

## 3 验证

在命令行输入下面命令。

```python
python
import torch
torch.cuda.is_available()
```

结果如下图Fig. 4.所示，就证明安装成功。

{{< image src="1_4.png" caption="Fig. 4. pytorch-gpu test" width="640" height="320" >}}

{{< admonition >}}
由于前面已经执行过**conda activate pytorch1.8**命令，所以请确保你已经进入了pytorch1.8虚拟环境。
{{< /admonition >}}

