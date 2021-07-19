# Trivial Drive (Kotlin)

Sample for Google Play Billing Library version 4

# アプリ仕様
このプロジェクトは、GooglePlay課金ライブラリの使用方法を示すサンプルです。<br>

このアプリは、プレイヤーがガスを購入できるシンプルな「運転」ゲームアプリ。<br>
車にはガスを貯蔵するタンクがあり、プレイヤーが運転するとガスタンク内が減少します（一度に1/4タンク）。<br>
ユーザーは、赤い車を提供する「プレミアムアップグレード」を購入することもできます(アプリ内課金(in app))<br>
ユーザーは、「無限ガス」を購入することもできます。(定期購読(subscription))<br>
その定期購読がアクティブな間、ガスを消費せずに運転することが可能です。<br>
定期購読は　月または年単位で購入できます。<br>

# 前提条件
- [Documentation](https://developer.android.com/google/play/billing/billing_overview.html)

# Screenshots
<img src="screenshots/game-fragment-screenshot.png" width=320 /> <tb> <img src="screenshots/purchase-fragment-screenshot.png" width=320 />

# Getting Started
local.propertiesでbase64EncodedPublicKeyを指定しない場合に警告が出るので設定が必要です。<br>
base64EncodedPublicKeyは、購入署名の検証に使用されます。 <br>
GooglePlayデベロッパーコンソールでアプリケーションを作成し、一致するアプリ内購入SKU(購入可能アイテムの一意の識別子)を追加します。<br>
以下に手順を示します。<br>

# GOOGLE PLAY DEVELOPER CONSOLE上の操作


1. 以下のURLにアクアセスして、開発者コンソール上でアプリケーションを作成します<br>
   https://play.google.com/apps/publish/<br>
   <img width="1432" alt="スクリーンショット 2021-07-19 21 49 09" src="https://user-images.githubusercontent.com/16476224/126162131-0eb008c7-98ce-42f1-9f5b-036bc9cb9b21.png">


2. アプリケーションの公開鍵（base-64文字列）をコピーします。 収益化のセットアップ->ライセンスから確認可能<br>
<img width="1422" alt="スクリーンショット 2021-07-19 21 12 51" src="https://user-images.githubusercontent.com/16476224/126163227-c6a32480-270a-40a2-8ce0-9cc76f842a1a.png">
   

# プロジェクトのコードを修正する

3. local.propertiesを開いて、 base64EncodedPublicKeyにコピーした値を設定します<br>
   <img width="716" alt="スクリーンショット 2021-07-19 22 00 42" src="https://user-images.githubusercontent.com/16476224/126163554-11fb189d-777d-48c8-a1aa-6e77431f829a.png">

4. application IDを変更する（R.javaの参照も変更する）<br>
   [pull request](https://github.com/LeoAndo/play-billing-samples/pull/1)

5. 本番用署名ファイルを作成し、その署名ファイルを使ってApp Bundleを作成する
   <img width="362" alt="スクリーンショット 2021-07-19 22 19 06" src="https://user-images.githubusercontent.com/16476224/126166145-1d48a944-9d2f-4cf0-9f67-2d018d05540b.png">
[pull request](https://github.com/LeoAndo/play-billing-samples/pull/2)

# GOOGLE PLAY DEVELOPER CONSOLE上の操作

6. 内部テストのためにApp BundleをGooglePlayにアップロードし、テスターを追加する
   これらのアカウントはテスト購入を行うことができます<br>
   <img width="1142" alt="スクリーンショット 2021-07-19 22 36 51" src="https://user-images.githubusercontent.com/16476224/126168546-7c953a3a-a746-422c-9bd4-dca1e01a73ec.png">
   <img width="1273" alt="スクリーンショット 2021-07-19 22 37 29" src="https://user-images.githubusercontent.com/16476224/126168555-d3536e3d-8f6d-44ef-b8c2-c5cee4ab1ac9.png">


8. [アプリ内アイテム]で、次のproduct IDを使用して製品を作成します。
   ```
       premium, gas
   ```
   <img width="1410" alt="スクリーンショット 2021-07-19 22 51 12" src="https://user-images.githubusercontent.com/16476224/126170718-574837db-7636-44ab-b13b-17b37d69c0ff.png">

   価格設定は以下の範囲で設定すること！<br>
   <img width="435" alt="スクリーンショット 2021-07-19 22 48 50" src="https://user-images.githubusercontent.com/16476224/126170246-4eac9e03-e8c4-4ead-8476-b5273448825b.png">



9. [定期購読]で、次のIDを使用して定期購読アイテムを作成します。
   ```
       infinite_gas_monthly, infinite_gas_yearly
   ```
   <img width="1422" alt="スクリーンショット 2021-07-19 22 57 17" src="https://user-images.githubusercontent.com/16476224/126171634-a4b0a654-c22c-4056-b85d-4cc978b82a4f.png">



10. アプリを内部テストチャネルに公開する。 すぐにテストする準備ができているはず。<br>
 
# TEST THE CODE

11. デバッグ証明書で署名されたAPKを、テストアカウントを持つテストデバイスにインストールします。<br>
12. アプリ実行する<br>
13. 課金テストする！<br>

実際に購入した場合は、返金することができます。 内でテスター機能を使用できます<br>
課金されないテストGoogleアカウントを定義するためのGooglePlayコンソール。<br>
テスター機能を使用するときは、それぞれに追加された「テスト」言語を必ず探してください<br>
デバイスのUIとレシートで購入します。 「テスト」が表示されない場合は、必ず返金/キャンセルしてください。<br>

A NOTE ABOUT SECURITY
---------------------

This sample app implements signature verification but does not demonstrate
how to enforce a tight security model. When releasing a production application
to the general public, we highly recommend that you implement the security best
practices described in our documentation at:

https://developer.android.com/google/play/billing/security

In particular, you should set developer payload strings when making purchase
requests and you should verify them when reading back the results. This will make
it more difficult for a malicious party to perform a replay attack on your app.

Support
-------
If you've found an error in this sample, please file an issue:
https://github.com/googlesamples/android-play-billing/issues

Patches are encouraged, and may be submitted by forking this project and
submitting a pull request through GitHub.

License
-------
Copyright 2021 Google, Inc.

Licensed to the Apache Software Foundation (ASF) under one or more contributor
license agreements.  See the NOTICE file distributed with this work for
additional information regarding copyright ownership.  The ASF licenses this
file to you under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License.  You may obtain a copy of
the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  See the
License for the specific language governing permissions and limitations under
the License.

CHANGELOG
---------

   2012-11-29: Initial release
   2013-01-08: Updated to include support for subscriptions
   2015-03-13: Updated to new dev console and added yearly subscriptions
   2015-08-27: Ported to gradle and prepped for transitioning to GitHub
   2021-04-28: Rewritten and updated to support Google Play Billing Library V3
