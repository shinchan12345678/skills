---
name: javascript-typescript-jest
description: "JavaScript / TypeScript の Jest テストを書く、更新する、レビューするときに使う。テスト構造、mock、async test、matcher、外部依存の分離を扱う。"
---

# JavaScript TypeScript Jest

## 方針

- `describe` / `test` / `it` の説明文は、既存テストに合わせる。迷う場合は日本語で書く。
- テスト名は「条件」と「期待する結果」が分かる名前にする。
- テストコメントは原則書かない。意図がテスト名や expect だけで伝わらない場合だけ、1行で理由を書く。
- Arrange / Act / Assert コメントは、既存テストで使われている場合だけ合わせる。
- 外部依存は mock し、テスト対象の振る舞いを分離する。
- async 処理は `async/await` または `resolves` / `rejects` で検証する。
- mock の呼び出し、返却値、例外など外から観測できる結果を検証する。
- mock の呼び出し確認では、可能な限り `toHaveBeenCalledWith` で重要な引数も検証する。
- 実装詳細の private な途中状態ではなく、公開 API の戻り値や副作用を検証する。

## Mock の使い分け

- Lambda が import する AWS SDK、外部 API client、別リポジトリの layer は、原則 `jest.mock()` で module 単位に mock する。
- mock module 内の関数は `jest.fn()` で定義する。
- テストケースごとの差分は、`jest.mock()` で用意した mock 関数の返却値や実装をそのテスト内で上書きする。
- mock の呼び出し履歴がテスト間で干渉する場合は、`afterEach` で clear する。
- `jest.spyOn()` は、実 module を読み込んだまま特定関数だけ監視または一時差し替えしたい場合に限る。

## よく使う検証

- 値: `toBe`, `toEqual`
- 文字列: `toMatch`, `toContain`
- 配列: `toContain`, `toHaveLength`
- object: `toHaveProperty`
- 例外: `toThrow`
- mock: `toHaveBeenCalledWith` を優先し、引数が重要でない場合だけ `toHaveBeenCalled`
