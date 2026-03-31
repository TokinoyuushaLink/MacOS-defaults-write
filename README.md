# MacOS-defaults-write
自用的macOS defaults write 合集，针对macOS sequoia

# 三指拖移
> 开启三指拖移以后，拖完东西延迟一会才结束
> ```bash
>defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadThreeFingerDrag -float 0.1
>```
>改回来：
>```bash
> defaults delete com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadThreeFingerDrag
>```

# 显示隐藏文件
> 开启隐藏文件
>
> ```bash
> defaults write com.apple.finder AppleShowAllFiles -bool true
> killall Finder
> ```
> 改回来
> ```text
> defaults write com.apple.finder AppleShowAllFiles -bool false
> killall Finder
> ```
# 启动台图标大小和列数
> 更改启动台图标为8列5行
> ```bash
> defaults write com.apple.dock springboard-columns -int 8
> defaults write com.apple.dock springboard-rows -int 5
> defaults write com.apple.dock ResetLaunchPad -bool TRUE
> killall Dock
> ```
> 改回来
> ```bash
> defaults write com.apple.dock springboard-rows Default
> defaults write com.apple.dock springboard-columns Default
> defaults write com.apple.dock ResetLaunchPad -bool TRUE
> killall Dock
> ```
> 针对sequora可能的重制方式
> ```bash
> sudo find /private/var/folders/ -type d -name com.apple.dock.launchpad -exec rm -rf {} +; 
> killall Dock
> ```

# 更改支持使用ESC键退出的app行为（好像没有什么用）
> 更改全局esc键行为（仅支持的app）
> ```
> defaults write NSGlobalDomain AppleESCKeyBehavior -int 2
> killall SystemUIServer
> ```

# 更改Dock栏隐藏的app图标透明度
> 隐藏程序图标半透明
> ```
> defaults write com.apple.Dock showhidden -bool YES
> killall Dock
> ```

# 更改特定的 app 全屏时的状态栏隐藏与否
> 隐藏app全屏时的状态栏隐藏
> 首先，查询你要操作的app的bundleID
> ```
> osascript -e 'id of app "你的程序"'
> ```
> > 例如：照片.app
> > ```
> > osascript -e 'id of app "Photos"'
> > ```
> >那么他将会返回
> > ```
> > com.apple.Photos
> > ``` 
> 记住返回的bundleID，填充进 `<bundle id>` 中
> ```
> defaults write <bundle id> AppleMenuBarVisibleInFullscreen -bool false
> ```
> 想要改回来
> ```
> defaults delete <bundle id> AppleMenuBarVisibleInFullscreen
> ```
> > 目前已经更改的app
> > - IINA : `com.colliderli.iina`
> > - 照片 : `com.apple.Photos`
> > - 哔哩哔哩 : `com.bilibili.bilibiliPC`
> > - 图书 : `com.apple.iBooksX`
> > - Typora：`abnerworks.Typora`
> > - Readest：`com.bilingify.readest`
> > - Diarly：`com.pureformstudio.diaryOSX-setapp`

# 更改Apple iWork软件更新提示
> 停止iWork软件在启动时的更新提示
> ```shell
>  defaults write com.apple.iWork.「Pages/Keynote/Numbers」 'TrialOfferIneligible' -bool TRUE
>  ```
>  全局方法：
>  ```shell
> sudo defaults write /Library/Preferences/com.apple.iWork 'TrialOfferIneligible' -bool TRUE
>  ```

## 关闭Gatekeeper
> 关闭联网认证
> ```
> sudo spctl --master-disable
>  ```
>  打开
>  ```
>  sudo spctl --master-enable
>  ```

# 在终端使用sudo的时候使用指纹
> 终端sudo使用指纹
> 在 `/etc/pam.d/` 里创建一个 `sudo_local` 文件，写入`auth    sufficient    pam_tid.so`

# 使用ctrl+command拖动窗口
> 使用ctrl+command在窗口的任意位置拖动窗口
> ```shell
> defaults write -g NSWindowShouldDragOnGesture -bool true
> ```
> 重新打开窗口生效



