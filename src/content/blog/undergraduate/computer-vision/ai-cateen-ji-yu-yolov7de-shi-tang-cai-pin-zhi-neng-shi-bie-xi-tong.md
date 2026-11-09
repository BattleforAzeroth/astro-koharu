---
title: AI Cateen(基于YOLOv7的食堂菜品智能识别系统)
link: ai-cateen-ji-yu-yolov7de-shi-tang-cai-pin-zhi-neng-shi-bie-xi-tong
date: 2023-04-07 09:29:00
categories:
  - - 本科作业
    - 计算机视觉
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/AI%20Canteen.cover.png
tags:
  - 计算机视觉
  - 目标检测
  - Android
---

:::info
使用目标检测技术实现更快捷方便的点单方式
基于 ncnn 实现的 Yolov7 网络安卓端部署，并实现了实时推理
21 类菜品的目标检测，并包含点单界面
:::

{% links %}
- site: AI Cateen(基于 YOLOv7 的食堂菜品智能识别系统)
url: https://github.com/BattleforAzeroth/AICanteen
desc: github 仓库
image: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/icons/GitHub.png
  color: "#24292f"
{% endlinks %}

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/AI%20Canteen.1.gif#pic_center)

# 安装

只需使用 Android Studio 打开此项目，项目中已经包含 NCNN 和 OpenCV 库

## 如果您需要更改库版本

- https://github.com/Tencent/ncnn/releases

1. 下载`ncnn-YYYYMMDD-android-vulkan.zip`或者自行构建 NCNN
2. 将`ncnn-YYYYMMDD-android-vulkan.zip`解压到`app/src/main/jni`，并在`app/src/main/jni/CMakeLists.txt`文件中更改 ncnn_DIR 路径

- https://github.com/nihui/opencv-mobile

1. 下载`opencv-mobile-XYZ-android.zip`
2. 将`opencv-mobile-XYZ-android.zip`解压到`app/src/main/jni`，并在`app/src/main/jni/CMakeLists.txt`文件中更改 OpenCV_DIR 路径

# 使用自定义数据

## 训练模型和模型转换

1. 训练 YOLOv7-tiny 网络模型
2. 将模型转换为 NCNN 格式，放在`app/src/main/assets`中，我个人的转换方法是使用[PNNX](https://github.com/pnnx/pnnx)

## 映射数组

定义在`app/src/main/java/com/tencent/ncnnyolov7/MenuActivity.java`中

```java
f = new int[]{1, 2, 3, 15, 20, 21, 4, 22, 16, 5, 6, 7, 8, 9, 10, 17, 11, 12, 23, 18, 13};
```

此数组解决了模型中与点单界面中类别号不对应的问题

## 菜品详细信息

菜品信息存放于本地，位于`app/src/main/res/values/strings.xml`中名为`eleme_json`的 json 字符串，图片通过 url 获取

更多信息请参考[Linkage-RecyclerView](https://github.com/KunMinX/Linkage-RecyclerView)

# 参考

数据集: [https://universe.roboflow.com/skoopin-data/pandadata](https://universe.roboflow.com/skoopin-data/pandadata)

YOLOv7: [https://github.com/WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7)

YOLOv7 安卓端部署: [https://github.com/xiang-wuu/ncnn-android-yolov7](https://github.com/xiang-wuu/ncnn-android-yolov7)

点单界面架构: [https://github.com/KunMinX/Linkage-RecyclerView](https://github.com/KunMinX/Linkage-RecyclerView)
