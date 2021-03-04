# README

#  original_app
### オリジナルのランキングが作成でき、集計を取れるアプリケーション

# 概要
### 誰でも簡単にランキングを作成することができる。
### 気になる分野の集計を取れ、マーケティングに役立つ

# 利用方法
#### `☆ トップページから新規登録・ログイン`
#### `☆ 一覧画面へ遷移する`
#### `☆ ランキングを投稿することができる`
#### `☆ ランキング投稿完了後は一覧画面へ戻る`
#### `☆ ランキング投稿詳細画面へ遷移する`
#### `☆ ランキング投稿者本人であれば投稿の編集・削除が投稿詳細画面から可能になる`
#### `☆ ランキング詳細画面から投票ができる`

# 課題解決

# 機能一覧
| 機能           | 概要             |
| -------------- | -----------------|
| ユーザー管理機能　| 新規登録・ログイン・ログアウトが可能  |
| 投稿機能 | ランキング投稿が可能 |
| 投稿詳細表示機能 | 各投稿詳細が詳細ページで閲覧可能 |
| 投稿編集・削除機能 | 投稿者本人のみ投稿編集・削除が可能 |
| 投票機能 | 投稿詳細ページから非同期通信で投票が可能|

# 追加予定機能

# 投票機能
| 特徴            | 概要             |
| -------------- | ---------------- |
| ランキングに関する投票の位置関係 | 気になる子要素に投票することができる　|
| 非同期通信活用 | 通信量の削減が可能となり、パフォーマンスの向上 |
 
# ローカルでの動作方法
$ git clone 
</br>
$ cd global-day
</br>
$ bundle install
</br>
$ rails db:create
</br>
$ rails db:migrate
</br>
$ rails s
</br>

# 開発環境
- VScode
- Ruby 2.6.5
- Rails 6.0.3.4
- mysql2 0.5.3
- JavaScript
- gem 3.0.3
- heroku 7.46.0

# DB設計

# users テーブル
| Column              | Type     | Options                   |
| ------------------- | -------- | ------------------------- |
| email               | string   | null: false, unique: true |
| encrypted_password  | string   | null: false               |
| nickname            | string   | null: false               |

### Association
- has_many :ranking_users
- has_many :ranking, through: ranking_users
- has_many :votes


# rankings テーブル
| Column     | Type          | Options     |
| ---------- | ------------- | ----------- |
| title      | string        | null: false |
| child_name | string        | null: false |

### Association
- has_many :ranking_users
- has_many :users, through: ranking_users
- has_many :votes


# ranking_users テーブル
| Column      | Type       | Options                        |
| ----------- | ---------- | ------------------------------ |
| user        | references | null: false, foreign_key: true |
| ranking     | references | null: false, foreign_key: true |

### Association
- belongs_to :ranking
- belongs_to :user


# votes テーブル
| Column     | Type          | Options     |
| ---------- | ------------- | ----------- |
| vote       | string        | null: false |

### Association
- belongs_to :ranking
- belongs_to :user
