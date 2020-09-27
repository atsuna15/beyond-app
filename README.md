# README

## アプリケーション名
beyond-app

## アプリケーション概要
ネット環境があれば、誰でも、自分の学びたいジャンルを学びたい人から学ぶことができる。
また、自らの知識や技術を生かして、誰かに伝えたい人が教える立場として参加できる。

## URL
デプロイ後記述する

## テスト用アカウント
未実装

## 目指した課題解決
学びたい。成長したいというニーズに応え、生まれた地域や環境によっての学習環境を差を少なくする。

## 洗い出した要件

### ユーザー登録・認証機能
- ユーザーアカウントの登録をする際、ユーザーは、閲覧者か投稿者のどちらとして登録するかを選択する。

### 動画投稿機能
- 投稿者アカウント登録したユーザーのみが動画を投稿することができる。
- 閲覧者アカウント登録したユーザーのみが閲覧できて、未ログインユーザーは閲覧できない。

### ルーム機能
- 閲覧者ユーザーは、自分でジャンルを選択し、ルームに入室できる。
- ルームに入ったユーザーのみがそのジャンルでの情報が得られる。
- ルームでは、動画視聴の他に、投稿者との連絡をできるようチャット機能もできるようにする。

### 多言語翻訳機能
- 対応可能な言語は、日本語、英語、スペイン語として実装を進める。

### クレジット決済機能
- 動画を商品として購入。動画がなければ購入できない。

- 「商品購入ボタン」をクリックしたら、DB及びPAY.JPサイトに購入した商品情報が更新される

- 購入済み動画は購入したユーザーは何度でも視聴できる。

## 実装した機能についてのGIFと説明
未実装

## 実装予定の機能
ユーザー登録・認証機能

## データベース設計
https://gyazo.com/8d8a78b253c680f3dab3f42f518bcf00

# テーブル設計

## students テーブル

| Column       | Type    | Options     |
| ------------ | ------- | ----------- |
| nickname     | string  | null: false |
| family_name  | string  | null: false |
| first_name   | string  | null: false |
| email        | string  | null: false |
| password     | string  | null: false |
| birth        | date    | null: false |
| nationality  | integer | null: false |
| image        | string  |             |

### Association 

- has_many :room_students
- has_many :rooms, through :room_students
- has_many :messages

## teachers テーブル

| Column       | Type    | Options     |
| ------------ | ------- | ----------- |
| nickname     | string  | null: false |
| family_name  | string  | null: false |
| first_name   | string  | null: false |
| email        | string  | null: false |
| password     | string  | null: false |
| birth        | date    | null: false |
| nationality  | integer | null: false |
| image        | string  |             |

### Association

- has_many :room_teachers
- has_many :rooms, through :room_teachers
- has_many :messages
- has_many :videos

## rooms テーブル

| Column       | Type    | Options     |
| ------------ | ------- | ----------- |
| name         | string  | null: false |

### Association

- has_many :room_teachers
- has_many :teachers, through :room_teachers
- has_many :room_students
- has_many :rooms, through :room_students
- has_many :messages

## videos テーブル

| Column       | Type       | Options                        |
| ------------ | ---------- | ------------------------------ |
| video        | string     | null: false                    |
| teacher      | references | null: false, foreign_key: true |

### Association

- belongs_to :teacher

## messages テーブル

| Column  | Type       | Options                        |
| ------- | ---------- | ------------------------------ |
| content | string     |                                |
| teacher | references | null: false, foreign_key: true |
| student | references | null: false, foreign_key: true |
| room    | references | null: false, foreign_key: true |

### Association

- belongs_to :teacher
- belongs_to :student
- belongs_to :room


