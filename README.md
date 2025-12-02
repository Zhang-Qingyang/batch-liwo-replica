# Batch-LIWO复刻项目

尝试根据公开信息复刻中科大RoboWalker战队2025赛季未开源的Batch-LIWO里程计。

本项目Fork自point_lio_ros2，感谢point_lio原作者和ros2移植开发者的贡献。

## 资料汇总

1.论坛开源提供的技术报告和Batch-LIWO论文：https://bbs.robomaster.com/article/803727

2.RMUC2025青工会技术分享：https://www.bilibili.com/video/BV1E44RzqEoy

3.Point-LIO原始论文

## 开发计划

截至目前（2025/12/2），中科大25赛季哨兵导航仍然没有任何一项技术的代码仓库有开源更新，所以只能从point_lio开始自己手搓。

batch-liwo在point_lio的基础上开发，主要有2个创新点

## 进度更新
2025/12/3

1.fork point_lio_ros2项目，准备开始开发

2.原项目没有完整支持MID360，重写了preprocess.cpp中部分内容，支持获取MID360提供的标准PointCloud2点云

目前已经能够跑通原项目，定位等功能均正常，实测平均CPU占用率（仅运行Point-LIO）在30%上下，偶尔有一两个核会飘到50%以上