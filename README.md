## 本アプリケーションの概要

<img width="400" alt="bench-map-logo" src="https://user-images.githubusercontent.com/54522567/115035136-36ecad00-9f07-11eb-87de-a88b2a4abdb3.PNG">

###### URL： https://bench-map.herokuapp.com
###### ログイン画面の「テストログイン」で１クリックでログインできます。
###### ※ ご覧になられた後は、お手数ですが、ログアウトをお願いいたします。

本アプリ『BenchMap』は、周辺のベンチを探せるWebアプリケーションです。  
マップにユーザーが登録したベンチが表示され、周辺のベンチを探すことができます。  
買い物などで歩き疲れたときに、座るためにカフェなどを利用するとお金がかかります。  
すぐにベンチなどの無料で座れる場所を探せたらいいのにと感じ、本アプリを開発しました。  


## 機能一覧および使用技術  

- ### フロントエンド  
  - Slim/Sass/Bootstrapを用いて作成し、レスポンシブデザイン化  
  - JavaScript (jQuery) およびAjaxを使用し、UX/UIの向上  
  - GoogleMapsに関する機能実装  
    - GoogleMaps表示機能  
    - ベンチの位置マーカー(以後、マーカー)の表示機能  
    - マーカーへのクリックによるベンチ情報表示機能  
    - GoogleMapsをクリックした地点に対する位置取得・登録機能  
    - 現在地取得・表示機能  
    - 地名検索・遷移機能  
    
- ### サーバーサイド(Rails)  
  - ベンチおよびその位置情報の取得・一覧表示機能  
  - ベンチの検索機能、ソート機能 (ransack, Ajaxで実装)  
  - ページネーション機能 (kaminari, Ajaxで実装)  
  - ベンチおよび位置情報の登録・編集機能  
  - ベンチへのいいね追加・削除機能  
  - べンチへのコメント投稿・編集・削除機能  
  - ユーザー登録機能 (Devise)  
  - Twitter、FacebookおよびGoogle アカウントでのログイン機能 (OmniAuth)  
  - ユーザー情報表示・編集機能  
  - 他ユーザーに対するフォロー機能  
  - ベンチおよびプロフィール画像の登録機能 (Active Storage)  

- ### API機能(Rails)  
  [モバイルアプリ (ReactNative (React / TypeScript) )](https://github.com/nakano0518/benchmap-for-mobile-README) のバックエンドとして実装  
  - ユーザー登録・ログイン・ログアウト機能 (Devise)
  - Twitter、FacebookおよびGoogle アカウントでのログイン機能 (koala, twitter)
  - その他、ベンチ・いいね・コメントに関するエンドポイント実装
  - 認証トークン生成・再生成機能 (simple_token_authentication)
  - JSONのシリアライズ機能 (active_model_serializers)
  - エラーハンドリング実装
  - CORS設定 (rack-cors)

- ### その他
  - 投稿されるベンチの画像を[機械学習モデル](https://github.com/nakano0518/benchImageClassifier)で判定しバリデーション

- ### テスト  
  約 200 テストケースを記述 (本アプリ完成時)  
  - 単体テスト (Rspec)  
  - 統合テスト (System Spec)  
  - 外部 API を利用した機能のテスト (モック / スタブの使用)  
  - カバレッジは約 90 % 以上を維持 (simplecov)  
　 
- ### インフラ  
  - #### 開発環境  
    - docker (docker compose) により構築  
  - #### 本番環境 
      **Amazon Web Service (AWS) により構築** 
    - EC2 インスタンスへのCICDパイプライン構築 (CircleCI (Rspec / Rubocop / Capistrano) )  
    - DB として、Amazon RDS (MySQL) を使用  
    - S3 を用いて、ベンチおよびプロフィール画像の保存場所を外部化  
    - Route53 で独自ドメインを設定し、ELB をエンドポイントとして常時 SSL 化  
    - 上記のインフラをコード化し [terraform で構築](https://github.com/nakano0518/IaC-for-AWS/tree/master/benchmap)  

    **⇒ AWSの無料利用枠の期限が満了したため、Herokuに移行しました。(2021.3.27)**

## 参考画像

### マップ画面  
<img width="800" alt="map-page" src="https://user-images.githubusercontent.com/54522567/115031240-e5daba00-9f02-11eb-9907-94bb4c2e723c.PNG">  

### ベンチ一覧表示画面  
<img width="800" alt="index-page" src="https://user-images.githubusercontent.com/54522567/115031269-ee32f500-9f02-11eb-9382-308ecea4bae2.PNG">  

### ベンチ詳細表示画面  
<img width="800" alt="show-page" src="https://user-images.githubusercontent.com/54522567/115031313-f8ed8a00-9f02-11eb-9e02-22b5fde7aaa7.PNG">  

### ユーザー詳細画面
<img width="800" alt="user-show-page" src="https://user-images.githubusercontent.com/54522567/115031330-fdb23e00-9f02-11eb-9a40-0cde1e396e35.PNG">  

### AWS インフラ構成図
<img width="500" alt="aws-infra-structure" src="https://user-images.githubusercontent.com/54522567/115034073-107a4200-9f06-11eb-93c1-73d31683c3bb.PNG">  

### ER 図
<img width="500" alt="er" src="https://user-images.githubusercontent.com/54522567/115033965-f6d8fa80-9f05-11eb-8d67-154a45e1ec34.PNG">  


