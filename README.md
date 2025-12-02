# Batch-LIWO复刻项目

尝试根据公开信息复刻中科大RoboWalker战队2025赛季未开源的Batch-LIWO里程计。

本项目Fork自point_lio_ros2，感谢point_lio原作者和ros2移植开发者的贡献，以及中科大的开源。

## 资料汇总

1.论坛开源提供的技术报告和Batch-LIWO论文：https://bbs.robomaster.com/article/803727

2.RMUC2025青工会技术分享：https://www.bilibili.com/video/BV1E44RzqEoy

3.Point-LIO原始论文

## 原理分析

截至目前（2025/12/2），中科大25赛季哨兵导航仍然没有任何一项技术的代码仓库有开源更新，所以只能从point_lio开始自己手搓。

由于要给原项目动手术，我们先从Point-LIO原项目的原理和整体工程组织开始，

Point-LIO的主要创新点在于Point Wise更新。相比其他LIO的逐帧更新（10Hz左右），一方面能够避免帧内运动畸变，另一方面极大提高输出带宽（200000Hz）。提高了鲁棒性，能够应对哨兵被撞等速度突变。

同时，Point-LIO相比FAST-LIO等传统方法，加入了状态量扩充。也就是，之前的Kalman滤波状态量只有位置、速度、姿态等，IMU读出的
角速度、加速度等直接当成input，如果出现IMU爆量程等现象就会导致观测异常。Point-LIO在状态量中直接加入了角速度和加速度，
如果IMU数据异常就降低置信度，用lidar的点云数据估计角速度和加速度，一定程度上提高了稳定性。而且因为采用逐点更新，lidar更新
频率远超IMU，这种方法就可以在IMU没数据的时候用lidar数据估计相关运动学状态。

batch-liwo在point_lio的基础上开发，主要3个创新点，

1.将逐点更新改为批量（Batch）更新

2.通过紧耦合Kalman滤波融合轮速数据

3.（在电控层实现的）底盘速度观测器

## 开发计划

## 进度更新

2025/12/3

1.fork point_lio_ros2项目，准备开始开发

2.原项目没有完整支持MID360，重写了preprocess.cpp中部分内容，支持获取MID360提供的标准PointCloud2点云

目前已经能够跑通原项目，定位等功能均正常，实测平均CPU占用率（仅运行Point-LIO）在30%上下，偶尔有一两个核会飘到50%以上