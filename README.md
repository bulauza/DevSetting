# 開発環境構築のための色々  
まっさらな状態から整えることを想定  
超個人的メモ

## やったことの理解
Windowsにはubuntuを動かすシステムがある=WSL(Windows Subsystem for Linux:WSL)  
しかしWSL上ではDockerが動かせない  
_because_ （無印の）WSLはlinuxカーネルが乗っていないから？  

そこでDocker for windowsを入れて，そこにpathを通す作戦（多分）  
WSL2だとこんなことをしなくていいかもしれない
←[参考](https://docs.microsoft.com/ja-jp/windows/wsl/wsl2-about#full-system-call-compatibility)  

## 問題点
[WSL/WSL2がGPUに対応していないため](https://docs.microsoft.com/ja-jp/windows/wsl/wsl2-faq#can-i-access-the-gpu-in-wsl-2-are-there-plans-to-increase-hardware-support)，  
今回の方法ではdocker内でGPUが使えなさそう(2019/12月時点)  
pythonとかのバージョン管理をホスト側に任せれば[リンク先](https://sekailab.com/wp/2019/03/10/execute-windows-binary-on-wsl/)
の方法が使えそうだが，  
スクリプト内でosとかsubprocessでbashのコマンドを使えない問題がある  
_because_ Windowsのpythonで動かすので，中で呼び出すコマンドもwindowsのものになってしまうから．

## Installation
### Windowsでubuntuを動かす(WSL)
1. Windowsマークで右クリック＞アプリと機能＞プログラムと機能＞Windowsの機能の有効化または無効化  
Hyper-VとWindows Subsystem for Linuxにチェックをつけてサインアウト  

1. Microsoft Store で ubuntuを検索・インストール  

### dockerも動かしたい
1. [docker hub](https://hub.docker.com/)からdesktopアプリをダウンロードする．  
1. Setting
    1. General で`Expose daemon on tcp://localhost:2375 without TLS`にチェック  
    1. Sared  Drivers でマウントするドライブを設定．  


## WSL内でdockerを使うための設定
[Docker for Windowsで快適な環境を得るまでの そこそこ長い闘い](https://qiita.com/YukiMiyatake/items/73c7d6c4f2c9739ebe60)  
[WSLでDocker for windowsを使うッ！！！](https://qiita.com/endo_hizumi/items/0cc50bdfbd827579733e)  

エラーが出てきてしまう
```
$ docker run --rm --gpus all nvidia/cuda nvidia-smi
docker: Error response from daemon: linux runtime spec devices: could not select device driver "" with capabilities: [[gpu]].
```
windowsだとまだdockerとgpu環境を共存させられなさそう
[参照](https://github.com/NVIDIA/nvidia-docker/issues/665)
