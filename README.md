# Awesome Lead Manager

## このアプリで何ができるか
- 見込み顧客（リード）の登録（Create）
    - 営業先や名刺交換した相手の情報を登録できる
    - 入力項目：名前（姓・名）、メールアドレス、会社名、メモ
- 顧客リストの一覧確認（Read）
    - 登録した顧客情報を一覧で確認できる
    - 最終更新日も自動で記録・表示される
- 情報の修正（Update）
    - メールアドレスが変わった、メモを追記したいといった具合に情報を編集できる
- 情報の削除（Delete）
    - 不要になった顧客データは削除できる
- 安全なアカウント管理
    - メールアドレスとパスワードで自分のアカウントを作成し、ログインすることにより自分専用のデータにアクセス可能


## アプリ作成の経緯
- Webアプリをバックエンドからフロントエンドまで作成し、一連の流れを学習したいという思いから教材を探した
- 教材としてhttps://youtube.com/playlist?list=PLhH3UpV2flrwfJ2aSwn8MkCKz9VzO-1P4&si=iTC4B62uK-CmGZ1dを使用

## 何が実装されているか
- フルスタック構成
    - バックエンド（Python/FastAPI）とフロントエンド（React）を完全に分離して開発
- RESTful API
    - HTTPメソッド（GET, POST, PUT, DELETE）を使い分けたAPI設計
- JWT認証（JSON Web Token）
- データベース操作（ORM）
    - SQLAlchemyを使用して、Pythonのコードでデータベースを操作

## 動作要件
- 開発環境はWindows11（via WSL2 / Ubuntu 24.04）
- FastAPIのバージョンについて（0.69.0）
    - 教材の安定性を重視し、教材がアップロードされた当時のバージョンで固定
- Pydantic（1.10.26）FastAPIに合わせて固定
- Python 3.12.3
- FastAPI 0.69.0
- Uvicorn 0.40.0
- SQLAlchemy 1.4.54
- See requirements.txt for full list