# homekit by esp8266
无需HomeBridge，使用esp8266直连HomeKit  
使用esp8266-01s连接苹果家庭App，控制继电器
# 下载
git clone https://github.com/LeeLulin/esp-homekit-direct.git  
```注意：使用之前需要先配置好 esp-open-sdk 的编译环境   
本项目示例型号为 esp8266-01s，如果使用其他型号，需要修改 /devices/switch/main.c 文件中的引脚定义
```
# 编译固件
```
cd esp-homekit-direct

make -C devices/switch all
```
编译完成会在 ```/devices/switch/firmware ```目录下生成 ```switch.bin```文件
# 刷写固件
##windows
1.安装```python```  
2.安装```esptool```  
```pip install esptool```  
3.把 /devices/switch/firmware 目录下的三个文件：rboot.bin blank_config.bin switch.bin 复制到python根目录下
4.清空Flash  
```esptool.py -p [端口] earse_flash
例：esptool.py -p COM3 earse_flash```
5.烧录固件
esptool.py -p [端口] -b 115200 write_flash -fs 1MB -fm dout -ff 40m 0x0 rboot.bin 0x1000 blank_config.bin 0x2000 switch.bin
