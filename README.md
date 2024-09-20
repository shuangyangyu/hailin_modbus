# Hailin Modbus 集成文档

## 简介

Hailin Modbus是一个Home Assistant自定义集成,用于连接和读取海林Modbus设备的数据。这个集成支持通过Modbus TCP协议读取PM2.5、温度和湿度数据。

## 起因

在网络中已有其他设备进行轮询的情况下,为了避免增加额外的网络负载,开发了这个插件。它只用于监听现有的Modbus通信,而不会主动发起轮询请求。

## 功能

- 通过Modbus TCP连接监听海林设备数据
- 解析并提供PM2.5、温度和湿度数据
- 提供配置流程,易于设置

## 安装

有两种方法可以安装此集成:

### 方法1: 使用HACS (推荐)

1. 确保您已经安装了[HACS](https://hacs.xyz/).
2. 在HACS中,转到"集成"标签.
3. 点击右上角的三个点,选择"自定义存储库".
4. 在"存储库"字段中输入: `https://github.com/shuangyangyu/hailin_modbus`
5. 在"类别"下拉菜单中选择"集成".
6. 点击"添加".
7. 关闭自定义存储库窗口.
8. 点击"+ 浏览并下载存储库"按钮.
9. 搜索"Hailin Modbus"并安装.
10. 重启Home Assistant.

### 方法2: 手动安装

1. 将`hailin_modbus`文件夹复制到您的Home Assistant配置目录下的`custom_components`文件夹中。
2. 重启Home Assistant。

## 配置

这个集成支持通过UI配置。按照以下步骤进行设置:

1. 在Home Assistant中,转到配置 > 集成。
2. 点击右下角的"添加集成"按钮。
3. 搜索"Hailin Modbus"并选择它。
4. 按照配置流程输入必要的信息。

配置项包括:

- 主机: Modbus设备的IP地址
- 端口: Modbus设备的端口号(默认为502)

## 传感器

这个集成会创建以下传感器:

1. PM2.5 (单位: μg/m³)
2. 温度 (单位: °C)
3. 湿度 (单位: %)

每个传感器都有唯一的ID和适当的设备类型。

## 工作原理

1. TCP监听: 集成使用`TCPService`类与Modbus设备建立TCP连接并监听数据。
2. 数据解析: `DataParser`类负责解析从Modbus设备接收到的数据帧。
3. 数据更新: `HailinTCPCoordinator`类管理数据更新过程,定期检查是否有新数据。
4. 传感器实体: `HailinModbusSensor`类表示每个传感器实体,并从协调器获取最新数据。

## 故障排除

如果遇到连接问题或数据读取错误,请检查以下几点:

1. 确保Modbus设备的IP地址和端口正确。
2. 检查网络连接是否稳定。
3. 确保有其他设备正在轮询Modbus设备,以便本集成可以监听到数据。
4. 查看Home Assistant的日志以获取更多错误信息。

## 贡献

如果您发现任何问题或有改进建议,请在GitHub上提交issue或pull request。

## 许可