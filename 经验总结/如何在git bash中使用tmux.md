1. 首先在 `msys2` 中下载 `tmux`
	- 先使用 `pacman -Syyu` 对 `msys2` 进行更新
	- 再使用 `pacman -S tmux`  下载相关文件
2. 将 `tmux.exe` 与 `msys-event-2-1-7.dll` `(C:\msys64\usr\bin)` 复制到 `git bash` `(C:\Program Files\Git\usr\bin)`文件夹下
3. 如果还是无法进行,则将上述文件夹一覆盖到上述文件夹二

*2022-07-17 周日*