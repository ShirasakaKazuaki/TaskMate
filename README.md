![Taskamte_logo](https://user-images.githubusercontent.com/63136727/84980476-29db2200-b16d-11ea-9d6c-bbe1ec4f95b8.jpg)

# TaskMate: タスク管理アプリ
---
Mathmate作成中に気になった点や、導入してみたかった技術を使って作成したタスク管理アプリです。
バックエンドをRuby on Rails、フロントエンドはVue.jsを採用し、RESTfulAPIを使って実装してあります。
デザインや機能性がかなり稚拙なものになってしまいましたが、Vue.jsとRESTfulAPIを使った実装についてはかなり理解を深めることができました。

## TaskMateの構成
---

### 構成
--- 
TaskMateはAWSに、次のような構成でデプロイしています。


#### インフラ環境
- EC2/ MySQL/ Nginx/ Unicorn
![Taskmate_構成](https://user-images.githubusercontent.com/63136727/84980152-42970800-b16c-11ea-8360-3f4c3a7a1f2a.jpg)


#### 言語/フレームワーク
- Ruby/ Ruby on Rails
- Scss/ Bootstrap
- Vue.js

#### 開発環境
- Docker
- docker-compose

### 機能一覧
---
- タスク投稿機能
- タスク完了機能
- 画面遷移（Ajax）
