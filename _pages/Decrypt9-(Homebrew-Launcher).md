---
title: "Decrypt9 (Homebrew Launcher)"
permalink: /decrypt9-(homebrew-launcher).html
---

現在、safehaxにバグが存在するため、3DSにカートリッジ（3DSゲーム、NDSゲーム、flashcartなど）が挿入されていないと動作しません。 一時的な回避策として、バージョン9.2.0以下3DSでは、 `Decrypt9WIP.3dsx` を `/3ds/` にコピーして、HBLからDecrypt9を直接実行することもできます。
{: .notice--info}

#### What you need

* 最新リリース版の[Decrypt9WIP](https://github.com/d0k3/Decrypt9WIP/releases/latest/)
* 最新フォークの[safehax+fasthax](https://gbatemp.net/attachments/safehax-fasthax-cb6a1bc-zip.73592/)

#### 手順

2. SDカード直下に `files9` フォルダが存在しない場合は作成
3. safehax+fasthax `.zip` の中身をSDカード直下にコピー。統合・上書きしてOK
3. Decrypt9WIPの `.zip` から `Decrypt9WIP.bin` SDカードにコピーし、ファイル名を `arm9.bin` に変更
3. SDカードを3DSに戻す
4. Homebrew Launcherを呼び出す
4. safehaxを選択して起動
4. 成功すれば、Decrypt9が起動します

[2.1.0 ctrtransfer](2.1.0-ctrtransfer) に続く
{: .notice--primary}
