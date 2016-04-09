# vtkCloudPoint
基于C#并使用vtk可视化工具的点云聚类、匹配功能的Winform软件


##完成的功能##
- 三维点云的文件（txt xls）的加载 树形文件管理 可视化缩放拖动[框架集成]
- 三维点云的含噪聚类 聚类基于2个参数 需要手动动态调整 算法自动辨别聚类Id 噪声ID为0
- 聚类结果基于聚类半径和聚类长宽比的剔除
- 聚类质心和真值物方值的匹配
- 各种预处理数据输出


##bugs known##
- 聚类效率捉急 分布式？应该可以 但是软件对象是standalone版本的 c++类库(boost等)？软件需求是C#版本的 调用类库？实践中…略复杂
- 若质心模式和真值模式异常类似 （棋盘风格）匹配易陷入局部最小值 而不是完美的匹配 若已知方向会比较好
- 非空 异常判断做的不够完善
- 功能模块和算法模块未分离和集成
- 还需加入调用MATLAB的模块


##核心算法##
+ 聚类使用含噪聚类算法DBScan 两个核心参数 半径阈值及阈值内点数 以符合条件的set为核心点进行拓展
+ 匹配使用ICP算法 一般依赖Ransac 以点找寻另一集合最近对应点进行判断不断进行迭代 解算 平移向量和旋转向量 知道均方误差小于某个阈值
+ 聚类半径和聚类长宽比剔除基于外接圆和外接矩形 
+ 以上算法都在c#下实现 烦躁
