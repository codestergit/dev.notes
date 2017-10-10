## 快捷键

cmd+shift+.  Finder里显示隐藏文件
Option+Command+Power  锁屏

## Iterm2
Auto-complete menu `cmd+;`
split screens  `cmd+d` (for vertical), `cmd+shift+d` (for horizontal)
new tab   `cmd+t`
Show paste history `cmd+shift+h`
Find the cursor `cmd+/`

打开允许任何来源
```
sudo spctl --master-disable
```
使用终端命令重建Spotlight索引的饿方式，可以将Mac下的所有磁盘全部重建索引，包括Mac本身的硬盘，磁盘镜像，还有外接硬盘等。  
```
sudo mdutil -E /
```
其实还可以选择重建某个文件的索引，或者某个文件夹目录也可以，首先我们需要直到这个文件或者文件夹目录的路径，之后替换到下面的命令中就可以了：
```
mdimport /path/to/file
# 重建欧路词典的索引
mdimport /Applications/Eudb_en_free.app
```

只选择重建Mac主磁盘
Macintosh HD的索引
```
sudo mdutil -E /Volumes/Macintosh\ HD/
```


重建某个外接磁盘的索引内容，当然要考虑替换外接磁盘的名字，这里的名字是“External”
```
sudo mdutil -E /Volumes/External/

关闭spotlight server的命令：sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist

打开spotlight server的命令： sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist

```
