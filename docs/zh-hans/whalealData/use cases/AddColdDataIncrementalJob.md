

#### 			添加冷数据增量作业

​	点击配置管理菜单下的表作业配置，在冷数据表作业页面点击蓝色新增按钮弹出以下表单，自行选择需同步的数据源库表与文件源，归档模式选择增量更新，需注意的是冷数据归档只可将MongoDB的数据归档。当归档模式为增量更新时需填写sql配置，可点击蓝色自定义sql按钮弹出第二张图所示表格选择完成条件后点击保存即可生成sql。表作业具有一致性校验功能，选择是后可填写所需校验的百分比，同步后平台将对同步的数据进行一致性校验。数据处理方式可选人工删除或系统删除，此功能在同步完成后将源表进行按后方批次进行删除。

![image-20230621140520679](../../../images/whalealDataImages/image-20230621140520679.png)

![image-20230621140550910](../../../images/whalealDataImages/image-20230621140550910.png)