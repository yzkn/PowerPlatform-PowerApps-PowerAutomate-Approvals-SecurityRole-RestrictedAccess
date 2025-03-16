# PowerPlatform-PowerApps-PowerAutomate-Approvals-SecurityRole-RestrictedAccess

Power Apps モデル駆動型アプリと Power Automate で実装した、セキュリティロールと所有権を厳密に設定した承認ワークフロー

---

# 制約事項

## ファイル列・画像列

Dataverseテーブルのファイル列・画像列を利用して添付ファイル機能を実現しようとする場合、他の種類の列と動作が異なることに注意を要する。

- レコードの新規作成時には、ファイル列・画像列にファイルをアップロードすることができない
  - 一度レコードを「保存」してから、「編集」することになるため、[セキュリティロールの特権](https://learn.microsoft.com/ja-jp/power-platform/admin/security-roles-privileges?tabs=new#table-privileges)として、「作成」だけでなく「書き込み」も必要となる
  - 「同一レコードに対して一度だけしかファイルを添付させない」というような仕様は（セキュリティロールだけでは）実現できない
  - 適切な機能を持つ外部ストレージと組み合わせるか、Base64エンコードしたうえで複数行テキスト型の列に登録する必要がある
- フォーム上のファイルの削除やアップロードは、フォームの保存時ではなく、即座に実行される
  - クラウドフローのトリガーでは、ファイルの変更を検知できない可能性がある

# 仕様の概要

## 申請機能

- 下書き保存
- コピー申請
- 代理申請
- ファイル添付

## 承認機能

- 多段階承認
  - 段階数の上限あり
  - 動的に段階数を指定 ×
- 承認段階のAND／OR設定 ×
- 引き上げ承認 ✕

## 検索機能

- 過去申請の検索
- 過去承認の検索
- 添付ファイルの検索

## 管理機能

- 個人設定
  - プロフィールの登録・変更
  - 印影画像の登録・変更

- マスタ管理
  - ユーザー情報の登録・変更（DataverseシステムテーブルのSystemUserテーブルに格納されない情報を管理）
    - 管理者の登録・変更
  - 役職の登録・変更（Entra IDの役職ではなく、独自に管理）
  - 部署の登録・変更（Dataverseの部署ではなく、独自に管理）
  - 承認ルートの登録・編集

# 申請項目

- 件名
- 優先度（通常／至急）
- 備考

---

# ソリューションパッケージ

| バージョン | 内容                    |
| ---------: | ----------------------- |
|      1.0.0 | Dataverseテーブルの定義 |
|            |                         |
|            |                         |


---

Copyright (c) 2025 YA-androidapp(https://github.com/yzkn) All rights reserved.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see <https://www.gnu.org/licenses/>.
