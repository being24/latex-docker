# Docker image for LaTeX
TeXLiveに様々な機能を追加したDocker imageです。

## Usage

[こちらのテンプレートリポジトリ](https://github.com/being24/latex-template-ja)と組み合わせて使用することを想定しています。
詳細は[こちら](https://zenn.dev/being/articles/how-to-use-my-latex)を参照してください。
ですが、それ以外の環境でも使用可能です。

コマンドラインからの場合、以下のように使用することができます。
カレントディレクトリにビルドしたいtexソースがあるとします．

```bash
docker run -u $(id -u):$(id -g) --rm -v $PWD:/workdir ghcr.io/being24/latex-docker latexmk main.tex
```

これでカレントディレクトリに `main.pdf` ができます．

## Version

タグは、年.月.リビジョンの形式で管理するように変更しました。
毎月のリリースを行う予定です。

| Image tag   | Ubuntu | TeXLive      | Arch         | Registry            |
| ---------   | ------ | -------      | -----------  | ------------------  |
| 3.0.3       | 20.04  | 2022         | amd64, arm64 | ghcr.io             |
| 3.1.0       | 20.04  | 2022         | amd64, arm64 | docker.io, ghcr.io  |
| 3.2.6       | 20.04  | 2022(frozen) | amd64, arm64 | docker.io, ghcr.io  |
| 3.2.8       | 20.04  | 2023         | amd64, arm64 | docker.io, ghcr.io  |
| 2023-frozen | 22.04  | 2023(frozen) | amd64, arm64 | ghcr.io             |
| 2024-frozen | 24.04  | 2024(frozen) | amd64, arm64 | ghcr.io             |
| 2025-frozen | 26.04  | 2025(frozen) | amd64, arm64 | ghcr.io             |
|latest-frozen| 26.04  | 2025(frozen) | amd64, arm64 | ghcr.io             |
| latest      | 26.04  | 2026         | amd64, arm64 | ghcr.io             |


## Author

being24

## License

MIT

## Pull Image

```bash
docker pull ghcr.io/being24/latex-docker:latest
```

## About Libraries of Special Note

* minted
  * listing系は導入や設定が煩雑だったりということもあり、モダンなライブラリとして採用しました。python3に依存するためdocker imageにから削除していません。

* siunitx
  * 何も考えずに単位を数式として表示すると斜体になってしまうなど不都合があります。これを回避するために導入しました。

* latexindent
  * latexソースコード用のformatterです。ソースコードのインデントを自動で揃えるようにしました。perlに依存するためdocker imageにから削除していません。

## PDF Version

論文等提出時に、PDFのバージョンが指定されている場合があります。
そういった場合、(u)platexであれば.latexmkrcの

```bash
$dvipdf = 'dvipdfmx %O -o %D %S';
```

を

```bash
$dvipdf = 'dvipdfmx -V 4 %O -o %D %S';
```

に変更することでバージョンを指定することができます。

## フォント
英語系のフォントはTeX Gyre Termesを、日本語系のフォントはHarano Ajiを使用しています。

## debug用のコンテナを起動する

```bash
docker run -it --rm --user root ghcr.io/being24/latex-docker:latest /bin/bash
```
