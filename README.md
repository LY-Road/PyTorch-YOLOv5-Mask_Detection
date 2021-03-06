# PyTorch-YOLOv5-Mask_Detection
● 使用YOLOv5实现口罩佩戴检测

训练100个epochs在验证集上效果：
Class|Images|Labels|Precision|Recall|mAP@.5|mAP@.5:.95
--|--|--|--|--|--|--
all|1569|3055|0.945|0.905|0.942|0.663
face_not_mask|1569|2199|0.926|0.852|0.907|0.593
face_mask|1569|856|0.965|0.957|0.978|0.733

### 配置环境
执行如下代码：
> $ pip3 install -r requirements.txt
### 下载数据集 
images：https://pan.baidu.com/s/1m-4Z80T4IBtJXrlJrRW9pg  提取码：zpbw  
labels：https://pan.baidu.com/s/1L-fYqoylbEKMyiKXCXz-7g  提取码：szqg
### 口罩数据集预训练模型
链接：https://pan.baidu.com/s/1hZpQl9EAjNRyvinVJEyWvQ 提取码：m52y  
将下载好的模型放在weights文件夹下。
### 数据处理
将下载好的images和labels放在data/mydata文件夹下，train.txt和valid.txt我已经生成好放在mydata文件夹下了。
### 修改配置文件
找到data/coco128.yaml，需要修改的内容如下：
> train: data/mydata/train.txt/   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  # 训练数据路径  
> val: data/mydata/valid.txt/     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  # 验证数据路径  
> nc: 2                            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # num_classes=2  
> names: ['face_not_mask','face_mask'] &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # claes_name  
### 训练
执行如下代码：
>$ python3 train.py --cfg yolov5s.yaml

加载预训练权重执行如下代码：
>$ python3 train.py --cfg yolov5s.yaml --weights weights/best.pt

### 测试
>$ python3 test.py --weights weights/best.pt

注意权重路径，记得把训练好的模型放在weights文件夹下。

### 检测
执行如下代码：
>$ python3 detect.py --weights weights/best.pt --source 0  &nbsp;&nbsp;&nbsp;&nbsp;# webcam  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; file.jpg &nbsp;&nbsp;&nbsp;&nbsp; # image   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; file.mp4&nbsp;&nbsp;&nbsp;&nbsp; # video  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path/  &nbsp;&nbsp;&nbsp;&nbsp;# directory  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path/*.jpg &nbsp;&nbsp;&nbsp;&nbsp; # glob  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; rtsp://170.93.143.139/rtplive/470011e600ef003a004ee33696235daa  &nbsp;&nbsp;&nbsp;&nbsp;# rtsp stream  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; rtmp://192.168.1.105/live/test &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # rtmp stream  
   
                            
其中0代表使用摄像头，可以选择图像、视频等。

### 参考代码
https://github.com/ultralytics/yolov5
