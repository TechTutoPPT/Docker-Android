[![](https://github.com/TechTutoPPT/Docker-Android/blob/main/IMG_8396.PNG)](https://youtu.be/s1MZsR3C3bs)

今天要跟大家介紹一個非常實用的開源項目Docker-Android, 這是一個將Android模擬器容器化的解決方案, 
讓我們可以在 Docker環境中快速部署, 測試和操作Android系統. 它的官方網址為:
```
https://github.com/budtmo/docker-android
```

它支援多種Android裝置型號與API版本, 並整合了VNC, ADB, 日誌共享等功能, 讓我們可以在瀏覽器中直接操作模擬器, 或透過命令列進行控制.
它能快速部署, 不論你是用Windows, MacOS或Linux只要支援Docker, 就能使用.
它能模擬Samsung Galaxy S6至S10, Nexus系列及Pixel C, API版本從Android 9至14.

在部署這Docker Android之前, 請執行以下指令確認該裝置是否支援虛擬化功能:
```
sudo apt install cpu-checker
kvm-ok
```

確認支援虛擬化功能並安裝Docker後, 執行以下指令便能快速部署:
```
docker run -d -p 6080:6080 \
  -e EMULATOR_DEVICE="Samsung Galaxy S10" \
  -e WEB_VNC=true \
  --device /dev/kvm \
  --name android-container \
  -v android_data:/home/androidusr \
  budtmo/docker-android:emulator_11.0
```

然後打開瀏覽器輸入http://localhost:6080就能看到模擬器畫面

我以ThinkPad X1 Carbon (i7-10510U CPU, 16GB RAM)於WSL Ubuntu中測試只可說能運行, 但效能不佳, 
故又嘗試降低模擬的裝置及Android版本:
```
docker run -d -p 6080:6080 \
  -e EMULATOR_DEVICE="Samsung Galaxy S6" \
  -e WEB_VNC=true \
  --device /dev/kvm \
  --name android-container \
  -v android_data:/home/androidusr \
  budtmo/docker-android:emulator_9.0
```
結果是暢順了不少, 但本想用作遊戲掛機的想法看來是實現不了, 我想這工具適合程式員作測試之用.


