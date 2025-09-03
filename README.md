# F1-CHS&ENG-Subtitle

**本字幕仅供参考学习，禁止商用**

**禁止将视频文件转发到各媒体平台**

**F1: The Movie（中译：F1: 狂飙飞车）精校中英特效字幕**

字幕由我个人制作 欢迎各位使用

使用字幕之前，请**务必安装**字体，字体文件在Fonts文件夹中

## 适配源

字幕对 **Apple TV的HDR版** 和 **Amazon的SDR** 版均做了适配

HDR版本

```
F1.The.Movie.2025.2160p.iT.WEB-DL.DDP5.1.Atmos.DV.HDR.H.265-BYNDR
```

SDR版本

```
F1.The.Movie.2025.2160p.AMZN.WEB-DL.DDP5.1.Atmos.H.265-BYNDR
```

## 字幕版本及如何选择

有注释版：后缀带有`.WithNotes`

无注释版：后缀带有`.WithoutNotes`

如果你是F1新粉 建议使用有注释版

如果你对电影中出现的相关现实人物及背景故事非常了解 想要获得更好的沉浸体验 建议使用无注释版

## 字幕的显示

由于ass字幕并不支持HDR，所以相关字幕的颜色设置均基于**MPV播放器**将HDR视频映射为SDR后所显示的色彩，无法保证在其他播放器中也能有准确的色彩

以下是我个人的MPV设置 以供参考

```mpv.conf 
# --- mpv.conf (用于 SDR 显示模式) --- #

###基础设置###
vo=gpu-next							# 基于libplacebo的实验性视频渲染器
hwdec=no							# 软件解码
profile=high-quality				# 更高质量的渲染设置
deband=yes							# 启用去色带算法
icc-profile-auto=yes				# 字幕随视频一起缩放并进行色彩管理

###播放功能设置###
fullscreen=yes						# mpv启动后直接进入全屏模式
keep-open=yes						# 播放或搜索到文件末尾时不要终止，相反，暂停播放器
save-position-on-quit				# 退出时始终保存当前播放位置
watch-later-options=start			# 稍后观看

###自动为 HDR 内容应用设置的配置文件###
[hdr-to-sdr]
profile-desc="Tone-map HDR video for SDR display"
profile-cond=get("video-params/colormatrix") == "bt.2020-ncl" or get("video-params/gamma") == "pq"

###色调映射设置###
tone-mapping=mobius					# mobius 更好的颜色准确性
```

```hdr.conf
# --- hdr.conf (用于 HDR 显示模式) --- #

###HDR 输出的通用设置###
vo=gpu-next						# 基于libplacebo的实验性视频渲染器
hwdec=no						# 软件解码
profile=high-quality			# 更高质量的渲染设置
deband							# 启用去色带算法
target-colorspace-hint=yes		# HDR直通

###播放功能设置###
fullscreen=yes					# mpv启动后直接进入全屏模式
keep-open=yes					# 播放或搜索到文件末尾时不要终止，相反，暂停播放器
save-position-on-quit			# 退出时始终保存当前播放位置
watch-later-options=start		# 稍后观看

###HDR10 视频播放###
[hdr-passthrough]
profile-desc="Native HDR10 playback"	
# 条件：是 HDR (bt.2020/pq) 但不是杜比视界
profile-cond=(get("video-params/colormatrix") == "bt.2020-ncl" or get("video-params/gamma") == "pq") and not (p["video-params/dolby-vision"] > 0)
tone-mapping=bt.2390			# 感知色调映射曲线（EETF），由 ITU-R 报告 BT.2390 指定
hdr-compute-peak=yes			# 分析视频内容来动态计算峰值亮度

###Dolby Vision 视频播放###
[dolby-vision]
profile-desc="Dolby Vision playback profile"
# 条件：是 杜比视界
profile-cond=p["video-params/dolby-vision"] > 0
gpu-api=d3d11					# Windows环境下，用 Direct3D 11处理HDR和杜比视界
hwdec=d3d11va					# 指定使用 D3D11VA 进行硬件解码
target-colorspace-hint=yes		# HDR直通
target-trc=pq					# 使用 PQ 伽马曲线
target-prim=bt.2020				# 使用 BT.2020 色域
vf=format:dolbyvision=yes		# 杜比视界滤镜
hdr-compute-peak=yes			# 分析视频内容来动态计算峰值亮度
tone-mapping=st2094-40			# 为处理包含动态元数据的内容而设计的色调映射算法

###SDR 视频上变换播放###
[sdr-to-hdr]
profile-desc="Upscale SDR video for HDR display"
profile-cond=get("video-params/colormatrix") ~= "bt.2020-ncl" and get("video-params/gamma") ~= "pq"
target-trc=pq					# 显示的传输特性为PQ
target-peak=auto				# 指定输出显示的测量峰值亮度为自动
inverse-tone-mapping=yes		# 允许反向色调映射（将 SDR 扩展到 HDR）
```


**本字幕由我个人制作 供参考学习，禁止商用**
