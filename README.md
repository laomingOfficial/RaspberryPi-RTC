# RaspberryPi-RTC
 Install DS3231 RTC on Raspberry Pi

 樹莓派本身是沒有RTC的，所以只要我們在沒連接網路的情況下把樹莓派開機，就會發現時間是錯誤的。為了解決這個問題，我們需要DS3132這類的RTC模塊，就可以讓樹莓派的時間像我們的台式電腦或筆電一樣，斷電後才保持計算正確的時間。

影片教學：未上傳

步驟：
1. 把DS3231接上樹莓派
2. 接上網線（請確保能上網），把樹莓派開機
3. 跟著影片裡的步驟
```
查看是否鏈接成功
sudo i2cdetect -y 1

把DS3231註冊在樹莓派裡
echo 'ds3231 0x68' | sudo tee /sys/class/i2c-adapter/i2c-1/new_device

查看DS3231的時間
sudo hwclock -r

把系統時間寫入DS3231
sudo hwclock -w

開機自動啟動RTC
sudo nano /etc/rc.local

在exit 0的上一行添加以下兩句指令
echo 'ds3231 0x68' | sudo tee /sys/class/i2c-adapter/i2c-1/new_device
sudo hwclock -s
```