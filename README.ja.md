| [English](README.md) | [Japanese](README.ja.md) |

# Esmpresso (エスプレッソ)

Esmpresso は ES Modules 時代のパッケージシステムです。
GitHub と GitLib で公開されているモジュールを扱う事ができます。

## Roast (publish)

ES Modules のコードを Esmpresso スタイルに変換できます。私達はこれをローストと呼んでいます。

1. GitHub Pages の設定を行います。
    - `Settings` -> `GitHub Pages` -> `Source` -> change to `master branch` and `save`
2. トップディレクトリに `.esm.conf.js` ファイルを追加し、`main` にエントリーポイントのパスを指定します。
3. リポジトリを https://esmpresso.com に登録します。

```js
// .esm.conf.js
export default {
  version: "0.0.1", // SemVer
  main: "index.js", // Entry point
};
```

ローストしたモジュールは世界に向けて出荷されます。

## Drip (import)

ローストされたモジュールを import し使用します。私達はこれをドリップと呼んでいます。

以下は動的にドリップするやり方です。

```html
<script type="module">
  const Modules = { // as Roasted Modules
    Foo: "https://uupaa.github.io/Foo/index.js",
  };

  (async() => {

  //const { default: Foo } = await import(Modules.Foo); // default export
    const { Foo } = await import(Modules.Foo); // named export

    console.log(Foo);
  })();
</script>
```

以下は静的にドリップするやり方です。

```html
<script type="module">
  (async() => {

  //import Foo from "https://uupaa.github.io/Foo/index.js"; // default export
    import { Foo } from "https://uupaa.github.io/Foo/index.js"; // named export

    console.log(Foo);
  })();
</script>
```

## FAQ

- Q. ES5 で書かれているスクリプトをローストするにはどうしたら良いですか?
    - A. まずは ES Modules スタイルに書き直す必要があります。

- Q. 他の人が公開しているモジュールをローストしたい場合はどうしたら良いですか?
    - A. リポジトリを fork して、ローストします。
        エントリポイント(index.js)に相当するファイルが存在しない場合は作成します。
        元のリポジトリにマージ依頼を出します。

