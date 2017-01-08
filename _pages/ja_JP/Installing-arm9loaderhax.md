---
title: "arm9loaderhaxのインストール"
permalink: /installing-arm9loaderhax.html
lang: ja_JP
lang: ja_JP
ref: installing-arm9loaderhax
---

このガイドの最後のステップは、arm9loaderhaxをインストールしてLuma3DSをセットアップすることです。これは[AuroraWright](https://github.com/AuroraWright/)が作成したSafeA9LHInstallerによって完了できます。
{: .notice}

このページでは、arm9loaderhaxの[AuroraWrightによる派生版](https://github.com/AuroraWright/arm9loaderhax)をインストールします。
{: .notice--info}

また、arm9loaderhaxからペイロードを起動する機能もセットアップし、バックアップからリストアすることによって通常は文鎮化するような状況からSysNANDを復活できるようにします。
{: .notice--info}

**別の本体のOTPを使用することはできません。使用した場合には必ず文鎮化します。**
{: .notice--danger}

#### このステップの概要

このページで、今までのステップが導いたプロセスを完了させます。実際にarm9loaderhaxをインストールします。

これは、NANDのファームウェアパーティションに永続的にインストール可能で、OSの大部分よりも早く実行されるため、どのバージョンでも動作します。さらに、機能していないホームメニューや悪いタイトルのインストールなど、A9LHが導入されていない3DSが文鎮化するような状況からでも復旧できる可能性が高くなります。

ファイル `arm9loaderhax.bin` は、arm9loaderhaxによってNANDがロードされた後に起動されるarm9ペイロードです。 このファイルはいつでも置き換えることができますが、Luma3DSを使用すると、設定したボタンを押しながら起動することで他のarm9ペイロード (Hourglass9など) を起動することができます。

この場合、[AuroraWright](https://github.com/AuroraWright/)が開発したLuma3DSを使用することで、EmuNANDを使用せずに、パッチを適用したSysNANDを直接起動します。SDカードのスペースを節約するだけでなく、ハック後の3DSの使用を大幅に簡素化します。

arm9loaderhaxのインストールに成功し、Luma3DSを正しくセットアップすることが出来れば、最後にバックアップを復元します。

併せて、次のようなソフトウェアもセットアップします。

+  **FBI** *(CIA形式のゲームや自作ソフトなどをインストール・管理)*
+  **Luma3DS Updater** *(CFWを簡単に更新)*
+  **Hourglass9** *(NANDやカートリッジを操作できる多機能ツール)*

#### 必要なもの

* [`aeskeydb.bin`](magnet:?xt=urn:btih:18b3a17f78e2376e05feaa150749d9fd689b25dc&dn=aeskeydb.bin&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)
* [`fbi-2.4.2-injectable.zip`](magnet:?xt=urn:btih:f978b4cf5eda72823240b9c649f3fd2940a9f525&dn=fbi-2.4.2-injectable.zip&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)
* [`data_input_v3.zip`](magnet:?xt=urn:btih:a1195c9f7ab650fa7c7bf020b51fc19ea8d9440c&dn=data%5Finput%5Fv3.zip&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=http%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fzer0day.ch%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969%2Fannounce&tr=http%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2Fexplodie.org%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2710%2Fannounce&tr=udp%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=http%3A%2F%2Fp4p.arenabg.com%3A1337%2Fannounce&tr=udp%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker.aletorrenty.pl%3A2710%2Fannounce&tr=http%3A%2F%2Ftracker1.wasabii.com.tw%3A6969%2Fannounce&tr=http%3A%2F%2Ftracker.baravik.org%3A6970%2Fannounce&tr=http%3A%2F%2Ftracker.tfile.me%2Fannounce&tr=udp%3A%2F%2Ftorrent.gresille.org%3A80%2Fannounce&tr=http%3A%2F%2Ftorrent.gresille.org%2Fannounce&tr=udp%3A%2F%2Ftracker.yoshi210.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.tiny-vps.com%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.filetracker.pl%3A8089%2Fannounce)
* 最新フォーク版の[SafeA9LHInstaller](https://github.com/Plailect/SafeA9LHInstaller/releases/latest) *(the `.7z` file)*
* 最新リリース版の[arm9loaderhax](https://github.com/AuroraWright/arm9loaderhax/releases/latest) *(the `.7z` file)*
* 最新リリース版の[Luma3DS](https://github.com/AuroraWright/Luma3DS/releases/latest) *(the `.7z` file)*
* 最新リリース版の[hblauncher_loader](https://github.com/yellows8/hblauncher_loader/releases/latest)
* 最新リリース版の[Hourglass9](https://github.com/d0k3/Hourglass9/releases/latest)
* 最新リリース版の[Luma3DS Updater](https://github.com/Hamcha/lumaupdate/releases/latest)
* 最新リリース版の[DspDump](https://github.com/Cruel/DspDump/releases/latest)
* 最新リリース版の[FBI](https://github.com/Steveice10/FBI/releases/)
* 最新リリース版の[GodMode9](https://github.com/d0k3/GodMode9/releases/latest)
* The Homebrew [Starter Kit](http://smealum.github.io/ninjhax2/starter.zip)

#### 手順

##### §1 - 準備

{% capture notice-5 %}
**お使いのSDカードが破損していないか確認してください。**

**破損しているSDカードを修正せずに使用すると、文鎮化することがあります！**

**SDカードが破損している可能性がある場合は、[H2testw (Windows)](h2testw-(windows))、[F3 (Linux)](f3-(linux))、[F3X (Mac)](f3x-(mac))を使用してSDカードのエラーをチェックしてください！**
{% endcapture %}

<div class="notice--danger">{{ notice-5 | markdownify }}</div>

1. **SDカードに `/ files9 /` フォルダが存在する場合、コンピュータ上の安全な場所にコピーして、複数の場所 (オンラインファイルストレージなど) にバックアップします。3DS本体のシステムが破損した際に、files9フォルダ内のファイルを使用して復旧することができます。**
2. SDカード直下に `cias` という名前のフォルダが無い場合、作成
4. **SDカード直下に `a9lh` フォルダがある場合、必ず削除**
  + **誤って別の本体の `OTP.bin` を使用してarm9loaderhaxをインストールした場合、文鎮化します！**
3. SDカード直下から `3ds` フォルダを削除
4. **SDカード直下に、 `starter.zip` の _中身を_ コピー**
  + このzipには、今削除したフォルダを置き換えるための `3ds` フォルダも含まれています
5. SafeA9LHInstallerの `.7z` の _中身を_ SDカードのルートにコピー
6. **data_inputの `.zip` から `a9lh` フォルダを取り出し、SDカードのルートにコピー**
7. **arm9loaderhaxの `release.7z`の内容をSDカードの` a9lh`フォルダにコピーしてください**
9. hblauncher_loaderの `.zip` から `hblauncher_loader.cia` を取り出し、SDカードの `/cias/` フォルダにコピー
10. Luma3DS Updaterの `.zip` から `lumaupdater.cia` を取り出し、SDカードの `/cias/` フォルダにコピー
11. FBIの `.zip` から `FBI.cia` を取り出し、SDカードの `/cias/` フォルダにコピー
12. **Luma3DSの `.7z` から `arm9loaderhax.bin` を取り出し、SDカード直下に上書きコピー**
13. SDカード直下に `luma` フォルダを作成
14. そのまま `luma` フォルダに入り、 `payloads` フォルダを作成
15. Hourglass9の `.zip` から `Hourglass9.bin` を取り出し、SDカードの `/luma/payloads/` フォルダにコピーして `start_Hourglass9.bin` に名前変更
16. GodMode9の `.zip` から `GodMode9.bin` を取り出し、SDカードの `/luma/payloads/` フォルダにコピーして `up_GodMode9.bin` に名前変更
16. SDカードの `/files9/` フォルダに `aeskeydb.bin` をコピー
17. SDカードの `/3ds/` に `DspDump.3dsx` をコピー
18. SDカードの `/files9/` フォルダに、 `fbi-2.4.2-injectable.zip` _の中身を_ コピー

##### §2 - arm9loaderhaxのインストール

1. SDカードを3DSに戻す
2. 下記の手順に沿って、3DS本体にarm9loaderhaxをインストール
  + 現時点で、3DSのシステムバージョンは2.1.0であるはずです
  + 3DSのインターネットブラウザーで `http://dukesrg.github.io/2xrsa.html?arm11.bin` にアクセス
    + 「このサービスはお住まいの地域では利用できません」のようにエラーが表示された場合は、本体設定を起動し、お住まいの国を2.1.0 ctrtransferファイルのものに設定します。
    + 他のエラーが表示された場合、[トラブルシューティングガイドを参照してください](troubleshooting#ts_browser)
    + 乱れた画面が表示された場合、[トラブルシューティングガイドを参照してください](troubleshooting#ts_safe_a9lh_screen)
  + (SELECT)ボタンを押してフルインストール
  + インストーラが3DS本体にarm9loaderhaxをインストールします (とても高速です)
  + 完了したら、いずれかのボタンを押して3DSの電源をシャットダウンします。オフにならなかった場合は、電源ボタン長押しでの強制電源断でも構いません
  + SDカードの `/a9lh/` フォルダから `OTP.bin` をあなたのコンピュータの安全な場所にコピーして、複数の場所 (オンラインファイルストレージなど) にバックアップする。そしてSDカードを3DSに戻す

##### §3 - Luma3DSを設定する

1. (SELECT)ボタンを押しながら3DSを起動し、Luma3DSの設定メニューに入る
  + 電源を入れる前から(SELECT)ボタンを押し続けてください
  + 真っ黒な画面になった場合、[このトラブルシューティングガイドを参照してください](troubleshooting#ts_sys_a9lh)   
  + SafeA9LHInstallerの画面が表示された場合、[このトラブルシューティングガイドを参照してください](troubleshooting#ts_safe_a9lh)
2. (A)ボタンと十字キーで操作し、次の項目をチェックを入れる
  + **"Autoboot SysNAND"**
  + **"Use SysNAND FIRM if booting with R"**
  + **"Show NAND or user string in System Settings"**
3. **New 3DS** を使用している場合、 *同じように* 次の項目を変更
  + **"New 3DS CPU" を "Clock+L2(x)" に**
    + これにより多くのゲームのフレームレートが向上しますが、他のゲームでは不安定になる可能性があります
    + ゲームが正常に動作しない場合は、この項目を "Off" にしてもう一度お試しください
4. (START)ボタンを押して保存・再起動
  + 真っ黒な画面になった場合、次のセクションに進みます
  + "Failed to mount CTRNAND" エラーが表示された場合、次のセクションに進みます

##### Section IV - システムの復元

既にEmuNANDを導入していて、そのデータをSysNAND CFWに移行したい場合は、ここで[EmuNANDの移行](move-emunand)を実行して、下記の手順1.から4.は実行せずスキップしてください。
{: .notice--info}

1. (START)ボタンを押しながら3DSを起動し、Hourglass9を呼び出す
2. "SysNAND Backup/Restore"、"SysNAND Restore (keep a9lh)" と進む
3. `NANDmin.bin` を使用して復元を行う
4. 完了したら、 (START)ボタンを押して再起動
  + 真っ黒な画面になった場合、[9.2.0 ctrtransfer](9.2.0-ctrtransfer)を実行してください
5. 復元したNANDバックアップのバージョンが3.0.0〜4.5.0の場合、必要なファームウェアを手動でダウンロードして配置するまで、コンソールは起動しません。
  + [このファイル](http://nus.cdn.c.shop.nintendowifi.net/ccs/download/0004013800000002/00000056)をダウンロードして `firmware.bin` にリネーム
  + [このファイル](http://nus.cdn.c.shop.nintendowifi.net/ccs/download/0004013800000002/cetk)をダウンロード
  + 入手した `firmware.bin` と `cetk` を、SDカードの `/luma/` フォルダにコピー
  + 3DSで「本体の更新」を行ったら、この２つのファイルは削除してください
2. 3DSを起動して本体設定を開き、「その他の設定」の最終ページにある「本体の更新」を実行
  + A9LHとLuma3DSを使用している状態での「本体の更新」は安全です、これについての質問や確認はしないでください
  + バージョン2.1.0のNew 3DSで本体更新をするなと警告しましたが、NANDバックアップを復元した後であれば問題ありません
  + 本体更新でエラーが発生した場合は、インターネット設定内のDNS設定を "自動" に設定してください。
  + 上記を行ってもエラーが発生し、NANDが9.2.0未満の場合は、[9.2.0 ctrtransfer](9.2.0-ctrtransfer)


##### §5 - 「安全に使用するために」をFBIに置き換え

1. (START)ボタンを押しながら3DSを起動し、Hourglass9を呼び出す
2. "SysNAND Backup/Restore"、"Health&Safety Dump" と進み、「安全に使用するために」を `hs.app` にバックアップ **(十字キーの上下左右を使うことで名前を指定できます。)**
3. 完了したら(B)ボタンを押して戻り、"Health&Safety Inject" へ進む
8. FBI置換用の `.app` を選ぶ
4. (A)ボタンで置換を実行
9. 完了したら、(START)ボタンで再起動
10. 「安全に使用するために」をまだ起動していて、過去にGATEWAY Launcherを使用してダウングレードしたことがある場合, [このトラブルシューティングガイドを参照してください](troubleshooting#gw_fbi)

##### Section VI - Finalizing setup

2. 「安全に使用するために」を起動 (現在FBIに置き換えているもの)
3. "SD" へ進む
4. "cias" へ進む
5. `FBI.cia` を開き、"Install" を選択して(A)ボタン → (A)ボタンでインストール
6. 同じように `hblauncher_loader.cia` をインストール
7. 同じように `lumaupdater.cia` をインストール
8. (B) ボタンで "SD" に戻る
8. `arm9loaderhax.bin` を開き、"Copy" を実行
9. (B)ボタンでFBIのメインメニューに戻る
10. "CTR NAND" へ進む
11. "\<current directory>" へ進む
12. "Paste" を選択して(A)ボタン → (A)ボタンで貼り付け
8. HOMEメニューに戻る
9. そのままHOMEメニューからHomebrew Launcherを起動
10. "DSP Dump" を選択して起動
11. (START)ボタンで終了するよう求められたら従う
12. 電源を切り、(START)ボタンを押しながら起動してHourglass9を呼び出す
13. "SysNAND Backup/Restore"、"Health&Safety Inject" と進む
14. 先ほどバックアップした `hs.app` (FBIを含んでいないもの) を選択し、(A)ボタンを押して置き換え
15. 完了したらメインメニューに戻り、(SELECT)ボタンを押してからSDカードを取り出す
15. SDカードを抜いたまま、(START)ボタンを押して再起動
  + SDカードを抜いた状態で初回起動を行うと、CTRNANDベースのLuma3DSの設定ができます
16. (A)ボタンと十字キーで操作し、次の項目をチェックを入れる
  + **"Show NAND or user string in System Settings"**
3. **New 3DS** を使用している場合、 *同じように* 次の項目を変更
  + **"New 3DS CPU" to "Clock+L2(x)"**
    + これにより多くのゲームのフレームレートが向上しますが、他のゲームでは不安定になる可能性があります
    + ゲームが正常に動作しない場合は、この項目を "Off" にしてもう一度お試しください
14. SDカードを3DSに戻し、(START)ボタンで保存・再起動して完了です！

___

DSi/DS関連の機能が破損している場合 (DSカートリッジやDSiウェアが機能しなくなったなど)、[このトラブルシューティングガイドを参照してください](troubleshooting#twl_broken)
{: .notice--warning}

{% capture notice-10 %}
Luma3DS Updaterを起動して(A)ボタンを押すだけで、Luma3DSを最新版にアップデートできます。
これは「本体の更新」とは異なり、最新のLuma3DSのファイルをダウンロードして抽出するものです。また、SDカードにあるファイルのみを更新します。
これにより、SDカード上のLuma3DSファイルのみが更新されます。SDカードなしでデバイスを起動すると、CTR NANDに配置したバージョンのLuma3DSが使用されます。
{% endcapture %}

<div class="notice--info">{{ notice-10 | markdownify }}</div>

{% capture notice-6 %}   
これで、CFWが導入されたSysNANDが起動するようになりました。
(SELECT)ボタンを押しながら起動することで、Luma3DSの設定メニューを呼び出せるようになりました。
(START)ボタンを押しながら起動することで、Hourglass9を起動できるようになりました。Hourglass9はarm9loaderhax用に作られた、NANDやカートリッジを操作できる多機能ツールです。
{% endcapture %}

<div class="notice--info">{{ notice-6 | markdownify }}</div>

今後、arm9loaderhaxを更新するには、[A9LHの更新](updating-a9lh)ページの指示に従ってください。
{: .notice--info}

[NTR CFW](https://github.com/44670/BootNTR/)を使用するには、[このページ](https://github.com/44670/BootNTR/releases)から適切な `.zip` を入手して `ntr.bin` を取り出し、それをSDカード直下にコピーして、最後に[このページ](https://github.com/astronautlevel2/BootNTR/releases/latest)にある `BootNTR.cia` を3DSにインストールします。
{: .notice--info}

`NANDmin.bin` ファイルは大切に保管しておいてください。文鎮化した際にHourglass9で復元することによって、3DSを救うことができます。
{: .notice--info}

NANDバックアップを安全な場所にバックアップしているならば、`/files9/` からNANDバックアップを削除しても構いません。
{: .notice--info}

{% capture notice-7 %}
**SDカードのルートから、次のリストに *ない* 余分なファイルやフォルダは削除して構いません。**

    + 3ds
    + files9
    + hblauncherloader
    + luma
    + Nintendo 3DS
    + arm9loaderhax.bin
    + boot.3dsx

{% endcapture %}

<div class="notice--info">{{ notice-7 | markdownify }}</div>

デバイスを別の地域に変更する方法については、[リージョンの変更](region-changing)ページを参照してください。
{: .notice--success}

インストールしたA9LHを最新に保つためには、[A9LHの更新](updating-a9lh)ページを参照してください。
{: .notice--success}

Luma3DSのさまざまな機能については、[このWiki](https://github.com/AuroraWright/Luma3DS/wiki/Options-and-usage)を参照してください。
{: .notice--success}
