# 開発環境構築のため手引き  
まっさらな状態から整えることを想定  
超個人的メモ

## ざっくり説明
WindowsにはWSLというLinuxを動かすシステムがある．  
WSL自体は前からあったが，  
今年6月17日あたりにWSL上でCUDAが使えるようになったのでGPUを使った学習が回せるようになった．  
基本的な導入はMicrosoftやNvidiaの公式ページを参照すれば良いが，  
所々すんなりいかなかったので共有する意図で書いていく．  
日本語情報としては[こちらの記事](https://qiita.com/ksasaki/items/ee864abd74f95fea1efa)が詳しい．  

## Installation
### Windows10 Insider Programのインストール
windowsの最新の機能を使うためのビルドをインストールする．  
具体的な手順は[こちら](https://qiita.com/ksasaki/items/ee864abd74f95fea1efa#windows-10-insider-preview-build-20150-%E4%BB%A5%E9%99%8D-%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)を参照．  
将来的には`wsl --install`で出来るようになるらしい．  

### WSLのインストール
1. **管理者**としてWindows PowerShellを開き，以下のコマンドを実行する．  
    ```powershell
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

    Restart-Computer # ここで再起動を忘れずに
    ```
1. WSL2を規定に設定する
    ```powershell
    wsl --set-default-version 2
    ```
1. Microsoft Storeから好きなLinuxディストリビューションをインストール  
使えるディストリビューションは[ここ](https://docs.microsoft.com/ja-jp/windows/wsl/install-win10#install-your-linux-distribution-of-choice)を参考

1. (Optional)インストール出来ているか確認  
    PowerShellで
    ```powershell
    wsl --list --verbose
    ```
    したときに名前の隣にversion2があれば大丈夫．
