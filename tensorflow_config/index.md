# 环境配置-tensorflow


Windows下tensorflow的GPU环境配置

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

## 2 安装tensorflow-gpu

如果没安装Anaconda，需先安装[Anaconda](https://www.anaconda.com/products/individual)，如果速度过慢可以复制下载链接到迅雷下载，或者使用[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/?C=M&O=D)。

### 2.1 预先准备

打开命令行输入**nvidia-smi**命令查看显卡驱动版本和CUDA版本，如下图Fig. 2.所示。

{{< image src="1_2.png" caption="Fig. 2. nvidia" width="640" height="320" >}}

{{< admonition >}}
这里的CUDA Version只是你目前对应的显卡驱动所支持的最高CUDA版本，意思后面你不能安装比这个版本高的CUDA。
{{< /admonition >}}

到[tensorflow官网](https://www.tensorflow.org/install/source_windows#gpu)查看所想安装的tensorflow-gpu与其对应的python、cuda和cudnn版本。
由于本人安装的是tensorflow-gpu-2.3.0版本，所以后面就以这个版本为例，如下图Fig. 3.所示。

{{< image src="1_3.png" caption="Fig. 3. tensorflow-gpu-2.3.0" width="640" height="320" >}}

{{< admonition >}}
由于tensorflow函数更新比pytorch大，所以选一个中间版本能稳定使用最好（如果后面要安装其它tensorflow版本，按部就班就行）。
{{< /admonition >}}

### 2.2 创建虚拟环境

tensorflow-gpu-2.3.0对应python版本区间为[3.5~3.8]，这里我选的3.7。

```conda
conda create -n tf2 python=3.7  
conda activate tf2              
```

### 2.3 安装tensorflow-gpu

```pip
pip install tensorflow
```

{{< admonition >}}
由于tensorflow-2.1及以上版本CPU和GPU软件包已经合并，不需要指定为tensorflow-gpu。
{{< /admonition >}}

### 2.4 安装cuda和cudnn

对于tensorflow-gpu-2.3.0版本来说，CUDA和CUDNN对应版本分别为10.1和7.6。

```conda
conda install cudatoolkit=10.1  
conda install cudnn=7.6.5       
```

## 3 验证

查看[tensorflow官网](https://www.tensorflow.org/versions/r2.3/api_docs/python/tf/test/is_built_with_cuda)api命令，在命令行下依次输入下面命令。

```python
python
import tensorflow as tf
tf.test.is_built_with_cuda()
tf.test.is_built_with_gpu_support()
```

结果如下图Fig. 4.所示，就证明安装成功。

{{< image src="1_4.png" caption="Fig. 4. tensorflow-gpu test" width="640" height="320" >}}

{{< admonition >}}
由于前面已经执行过**conda activate tf2**命令，所以请确保你已经进入了tf2虚拟环境。
{{< /admonition >}}

