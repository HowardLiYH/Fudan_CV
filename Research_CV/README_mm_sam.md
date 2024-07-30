# 说明
本项目代码目标为实现电力场景下基于大模型的分割，合并了一个目标检测模型（基于mmdetection的yolox）和一个剪枝后的SAM（SlimSAM）。训练与测试为二阶段形式：第一阶段，在电力场景数据集训练yolox，使其能够检测目标类别；第二阶段，将检测模型输出的检测框作为prompt训练SlimSAM，使其能够分割出检测框提示的物体。两个模型的各自详细信息可参考对应项目的github项目，论文，及tutorial。

# 数据
本项目数据使用电力场景下采集的原始图片与人工分割标注，数据原始形式，后处理代码，后处理后数据保存于`/media/jiawei/11223d19-7ce9-4280-b00c-81bb984d9872/jiawei/data/samples`文件夹中。`images_raw`与`labels_raw`存放原始数据，`train`与`validation`存放清洗后划分训练验证集后的数据。`*_annos.json`存放处理为coco检测格式的对应标签文件。

# YOLOX（mmdetection）
mmdetection为openmmlab提供的开源2D检测框架，熟悉后非常方便使用。安装、数据处理、训练、验证，官网提供了非常详细的双语文档，可供参考。我修改后的代码存放于`/media/jiawei/11223d19-7ce9-4280-b00c-81bb984d9872/jiawei/code_backup`中，更改了配置文件与训练、测试入口代码，训练与测试入口可简单使用`go.sh`与`test.sh`实现，进一步更改模型与实现更多模块请参考官方文档。数据软链接参考`data`文件夹下软链接与上一部分数据的介绍。修改代码最好将代码复制到自己工作空间下进行，留存一份原代码备份在此`code_backup`文件夹下。具体环境配置与训练测试，参考项目内README文件。

# SlimSAM（SAM）
我修改后的SlimSAM部分代码同样存放于`/media/jiawei/11223d19-7ce9-4280-b00c-81bb984d9872/jiawei/code_backup`中，主要更改了数据接口，prompt形式，以及提供了完整的从上一步训练好的检测模型输出检测框并输入SlimSAM进行分割的过程代码`inference_2stage.py`。同样，修改代码最好将代码复制到自己工作空间下进行，留存一份原代码备份在此`code_backup`文件夹下。具体环境配置与训练测试，参考项目内README文件。