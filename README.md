![status](https://img.shields.io/badge/status-live-brightgreen)
![stack](https://img.shields.io/badge/stack-Vue3%20%2B%20Laravel%20%2B%20PostgreSQL-blue)
[![demo](https://img.shields.io/badge/demo-open%20app-000)](https://rbplus-rank-manager.site)

## 目次
- [概要](#概要)
- [機能一覧](#機能一覧)
- [使用技術](#使用技術)
- [アーキテクチャ構成図](#アーキテクチャ構成図)
- [データベース構成](#データベース構成)
- [技術的な工夫点](#技術的な工夫点)
- [スクリーンショット](#スクリーンショット)
- [リポジトリリンク](#リポジトリリンク)
- [今後の展望](#今後の展望)


# REFLEC BEAT plus レベル11 難易度表＆クリアランク管理サイト

私は音楽ゲーム **REFLEC BEAT plus** が大好きです。  
しかし近年はプレイヤー人口が減り、SNSでは「オワコン」と言われることも増えています。  

「このゲームをもっと盛り上げたい」「プレイヤーのモチベーションを高めたい」  
そんな思いから、**難易度表とスコア管理を一体化したWebアプリ**を開発しました。  

- 難易度表をランクごとに整理し、進捗を可視化  
- 自分のスコアやフルコンボ状況を記録できる  
- Google Maps上で設置店舗を確認し、行脚記録も可能  

「自分が欲しいと思うサービスを、自分の力で形にする」  
その挑戦として、フロントからバックエンドまで一人で開発・公開しました。

## 概要
本プロジェクトは、音楽ゲーム **REFLEC BEAT plus**（iOS版）の「レベル11難易度表」と「クリアランク管理」を行うWebアプリです。  
難易度表の閲覧、スコア管理、店舗情報の可視化を通じて、プレイヤーのモチベーション向上とコミュニティの活性化を目的としています。  

- **URL**：[rbplus-rank-manager.site](https://rbplus-rank-manager.site)  
- **検証用アカウント**  
  - メールアドレス：`test@example.com`  
  - パスワード：`password`  

---

## 機能一覧

### 一般ユーザー向け
- 難易度表（非公式の地力ランク F〜S+）の閲覧
- 各曲に対するランク（AAA+/AAA/…）・フルコンボ状況・メモの保存
- フルコンボ時の演出表示（FULL COMBO!! / EXCELLENT!!!）
- フィルタ機能（ランク・FC/未FC）
- 進捗管理機能（目標ランクに対する達成率をプログレスバー表示）

### サービス拡張機能
- Google Maps APIによる店舗情報マップ表示
- ユーザーによる行脚記録（位置情報チェックイン）
- 行脚履歴一覧表示（訪問日時・店舗名など）

### 管理画面（Laravel Blade）
- 店舗一覧・検索・状態管理（公開/非公開）
- 店舗情報の編集（住所、緯度経度、台数、価格、説明文など）
- 論理削除（is_deletedフラグ）による安全なデータ管理
- ログイン認証・アクセス制御（管理者のみ利用可能）

---

## 使用技術

| 分類          | 使用技術・サービス                                      |
|---------------|---------------------------------------------------------|
| フロントエンド | Vue 3, Vite, TypeScript, Pinia, Vue Router, Axios     |
| バックエンド   | Laravel 12, Breeze, Sanctum, Blade                     |
| データベース   | SQLite（ローカル）, PostgreSQL（Render本番環境）       |
| インフラ       | Vercel（フロント）, Render（バックエンド/DB）, 独自ドメイン（ムームードメイン） |
| デザイン       | Figma（画面設計）                                     |
| その他         | Google Maps API, GitHub, ChatGPT                       |

---

## アーキテクチャ構成図
![Architecture](./public/Architecture-20250814.jpg)

- フロントは **Vue 3 + Vite** によるSPA（Vercelにデプロイ）  
- バックエンドは **Laravel 12**（Renderにデプロイ、Sanctum認証導入）  
- データベースは **PostgreSQL（Render）**  
- 管理画面は **Laravel Blade（SSR）** による別UIとして実装  

---

## データベース構成
![ER図](./public/er-diagram-20250814.png)

- users：ユーザーアカウント  
- songs：楽曲データ  
- scores：各ユーザーのスコア・ランク・FC状況  
- shops：設置店舗情報  
- user_visits：行脚履歴  

---

## 技術的な工夫点
- **SPAとBladeの併用**：一般ユーザー画面はSPA、管理者画面はBlade SSRで開発効率と保守性を両立  
- **SanctumによるSPA認証**：セキュアなログイン・ログアウト処理を実装  
- **Render無料枠対策**：Google Apps Scriptによる定期アクセスでスリープ防止  
- **論理削除フラグ**：実データを残しつつ公開/非公開を制御  
- **独自ドメイン運用**：`rbplus-rank-manager.site` を取得・設定  

---

## スクリーンショット
### 難易度表
![TIER](./public/tier.png)

### 店舗マップ
![MAP](./public/map.png)

### 管理画面（店舗一覧）
![管理画面一覧](./public/管理画面設置店舗一覧.png)

### 管理画面（店舗編集）
![管理画面編集](./public/管理画面設置店舗編集.png)

---

## リポジトリリンク
- [フロントエンド（Vue 3 + TS + Vite）](https://github.com/misato729/score-manager-frontend)  
- [バックエンド（Laravel 12 + Sanctum + Blade）](https://github.com/misato729/score-manager-backend)  

---

## 今後の展望
- Google Adsenseによる広告収益化（現在は忍者Admaxで代替）  
- Wiki的な静的コンテンツの追加（楽曲攻略情報など）  
- 管理画面にユーザー管理・楽曲管理機能を拡張予定  
- バグ修正・パフォーマンス改善（新規登録フォームの改善など継続中）

---
