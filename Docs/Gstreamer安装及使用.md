# Gstreamer Ubuntu18 安装

``` c++

sudo apt update
# 安装Gstreamer软件
sudo apt install gstreamer1.0-tools  gstreamer1.0-alsa  gstreamer1.0-plugins-base  gstreamer1.0-plugins-good  gstreamer1.0-plugins-bad  gstreamer1.0-plugins-ugly  gstreamer1.0-libav  gtk-doc-tools -y
# 安装Gstreamer开发包
sudo apt install libgstreamer1.0-dev  libgstreamer-plugins-base1.0-dev  libgstreamer-plugins-good1.0-dev  libgstreamer-plugins-bad1.0-dev  libgstrtspserver-1.0-dev -y

```

# 测试

``` shell 
gst-launch-1.0 -v videotestsrc pattern=0 ! "video/x-raw,framerate=30/1,width=800,height=600" ! timeoverlay ! autovideosink

```

https://blog.csdn.net/zhuyunier/article/details/90411669
