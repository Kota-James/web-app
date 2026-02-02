# 開発ログ

## 2026-02-02 (Day6)
- 体調不良により進捗なし

## 2026-02-01 (Day5)
- 1日バイトにより進捗なし

## 2026-01-31 (Day4)
- Building CRUD Endpoints
- いくつかtypoによるバグに苦しんだ

## 2026-01-30 (Day3)
- FastAPI User JWT Authentication


### ⚠️ トラブルシュート：非同期関数の呼び出し忘れ
**事象:**
APIを実行した際、`400 Bad Request` が発生し、ログに以下の警告が表示された。
`RuntimeWarning: coroutine 'get_user_by_email' was never awaited`

**原因:**
`async def` で定義された非同期関数（`get_user_by_email`）を呼び出す際に、`await` キーワードを付け忘れていた。
これにより、関数の実行結果（Userオブジェクト）ではなく、実行待ちの「コルーチンオブジェクト」が返却され、後続の判定処理（`if user:` など）が正しく機能しなかった。

**解決策:**
呼び出し元（`main.py`）で `await` を追記した。

python
# 修正前（NG）
user = services.get_user_by_email(email=user.email, db=db)

# 修正後（OK）
user = await services.get_user_by_email(email=user.email, db=db)


### ⚠️ トラブルシュート：PasslibとBcryptのバージョン競合
**事象:**
ユーザー登録（パスワードハッシュ化）を行おうとすると、以下のエラーが発生して 500 Error になる。
`ValueError: password cannot be longer than 72 bytes`
`AttributeError: module 'bcrypt' has no attribute '__about__'`

**原因:**
パスワードハッシュ化ライブラリ `passlib` が最終更新から時間が経っており、最新の `bcrypt (v4.0.0以上)` の仕様変更（`__about__` 属性の削除など）に対応できていないため。

**解決策:**
bcrypt のバージョンを v3系にダウングレード固定した。
`pip install "bcrypt==3.2.0"`


## 2026-01-29 (Day2)
- Creating Models with SQLAlchemy
バックエンドの基盤実装完了。 SQLAlchemyでのModel定義と、PydanticでのSchema定義（データの入出力設計）まで終わらせた。



## 2026-01-28 (Day1)
- プロジェクトの全体像を把握
    - 顧客管理システム
        - 認証システム
        - CRUD
        - ユーザーと見込み客のデータを紐づける
- Git等を設定

### 🔧 環境構築の特別対応：ライブラリのバージョン固定
**課題:**
教材動画（2021年公開）と現在（2026年）のライブラリ環境に大きな乖離があり、最新版をインストールすると互換性がなくコードが動作しない問題が判明。特に `Pydantic v2` と `SQLAlchemy 2.0` の破壊的変更が致命的だった。

**対応:**
動画のコードをそのまま再現するため、意図的にバージョンをダウングレードして固定した。

**実行したコマンド:**
bash
# 動画の時期に合わせてバージョンを指定（Pydantic v1系, SQLAlchemy 1.4系など）
pip install "fastapi<0.70.0" "pydantic<2.0.0" "sqlalchemy<1.5.0" "uvicorn[standard]" "passlib[bcrypt]" "python-multipart"