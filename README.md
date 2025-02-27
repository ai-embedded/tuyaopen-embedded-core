# tuyaopen-embedded-core
本项目是从 [tuyaopen](https://github.com/tuya/tuyaopen) 修改而来，将连接 tuya 云相关组件重新组织，方便嵌入至各种嵌入式平台使用。

## 下载
```shell
$ git clone https://github.com/ai-embedded/tuyaopen-embedded-core
$ git submodule update --init --recursive 
```
本项目采用 submodule 管理子仓库，执行时请使用 `--recursive` 参数。

## 依赖安装
```shell
$ sudo apt-get install -y cmake ninja-build
```


## 编译与运行
1. 修改 `TUYA_PRODUCT_KEY` `TUYA_OPENSDK_UUID` 与 `TUYA_OPENSDK_AUTHKEY`

请根据 [https://github.com/tuya/tuyaopen/blob/master/apps/tuya_cloud/README_zh.md](https://github.com/tuya/tuyaopen/blob/master/apps/tuya_cloud/README_zh.md) 获取 `TUYA_OPENSDK_UUID` 与 `TUYA_OPENSDK_AUTHKEY`。

2. 编译
```shell
$ cd demos/switch_demo
$ cmake -S . -B build -G "Ninja" && ninja -C build
```
 
3. 运行

```shell
$ cd demos/switch_demo
$ ./buildswitch_demo
```
首次运行时设备未激活，会自动弹出二维码，请使用 "智能生活" APP 扫码激活设备。
