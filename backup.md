# Linux系システムのバックアップ方法（Raspberry piでルーターを構成した際の方法)

## Raspbianに対してパッケージのアップグレードやシステムの変更をする際は、**必ずバックアップイメージを作成してから行うこと**
アップグレードをした後にシステムが動作しなかった時に、すぐに動作できる状態に戻すことが出来るようにするため。   
新しいバージョンにするときは、数日動作できることを確認した後にSDカードにバックアップする。   

## バックアップ方法 
1. ddコマンドを使用してimageファイルの作成
2. 設定済RaspbianをSD Card CopierでmicroSDカードにバックアップ


## 1.imageファイルによるバックアップ(他のLinux環境で実行)
- バックアップするSDカードをスロットに挿入
- SDカードのデバイス名を確認、以下のコマンドで表示する   
    >  sudo fdisk -l

    ~~~
    ディスク /dev/mmcblk0: 15 GiB, 16088301568 バイト, 31422464 セクタ
    単位: セクタ (1 * 512 = 512 バイト)
    セクタサイズ (論理 / 物理): 512 バイト / 512 バイト
    I/O サイズ (最小 / 推奨): 512 バイト / 512 バイト
    ディスクラベルのタイプ: dos
    ディスク識別子: 0x8193936a
    ~~~

- imgファイルとしてバックアップファイルを作成する
    > sudo dd bs=100M if=/dev/mmcblk0 of=\<FileName\>.img status=progress   
    
    if=バックアップするSDカードのデバイス名   
    of=バックアップの保存パスと名前    
    bs=バッファーサイズ   
    status=progress 進捗状況の表示   


- ## 復元の方法 (Linux環境で実行)
    **※バックアップしたSDカードと同じサイズのSDカードに復元すること**

    - imgファイルからSDカードに復元する
        > sudo dd bs=100M if=\<FileName\>.img of=/dev/mmcblk0 status=progress 
    
    if=バックアップファイル   
    of=復元先のSDカードのデバイス名    
    bs=バッファーサイズ   
    status=progress 進捗状況の表示   

## 2. SD Card CopierでmicroSDカードにバックアップ(Raspbian内で実行)
以下参照   
- [設定済RaspbianをSD Card CopierでmicroSDカードにバックアップ](https://www.fabshop.jp/%E3%80%90step-24%E3%80%91%E8%A8%AD%E5%AE%9A%E6%B8%88raspbian%E3%82%92sd-card-copier%E3%81%A7microsd%E3%82%AB%E3%83%BC%E3%83%89%E3%81%AB%E3%83%90%E3%83%83%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97/)