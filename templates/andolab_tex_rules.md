# 安藤研 TeXフォーマットルール

このファイルをCLAUDE.mdに記載しておくと、AIがTeXの修正時にこのルールに従ってくれます。

---

## 句読点・記号

- 「、」「。」は使わない。**「,」「.」に統一**
- 読点「,」の後には**半角スペース**を入れる
  - OK: `系統樹を推定することは, 重要な課題である.`
  - NG: `系統樹を推定することは,重要な課題である.`
- 文末ピリオドの前にスペースは入れない
- キャプション末尾には必ずピリオド「.」をつける
  - `\caption{グラフ $G$ の構造.}`

## スペーシング

- **半角と半角の間には半角スペース**を入れる
  - OK: `$k$SS操作 (Subtree Swap Operation)`
  - NG: `$k$SS操作(Subtree Swap Operation)`
- 括弧の外側にも半角スペースを入れる
- 引用 `\cite{}` の前には `~`（改行禁止スペース）を使う
  - OK: `Ailon et al.~\cite{AC11}は`
  - NG: `Ailon et al.\cite{AC11}は`
- 日本語と数式の間はスペースなしでもよい（TeXが自動調整）

## 数式

- オーダー記法は `\mathrm{O}` を使う: `$\mathrm{O}(n \log n)$`
- ローマン体にすべき関数名は `\mathrm{}` で囲む
- ノルムは `\|\cdot\|` で書く: `$\|D_{(T,h)} - M\|_2$`
- 条件付き最適化の制約は `\mathrm{s.t.}` を使う
- テキスト中の条件は `\text{}` を使う: `\text{if } p < \infty`
- 実数集合は `\mathbb{R}` を使う

## 図・表・アルゴリズム

- 画像形式は **EPS** を使う（tgif / gnuplot で生成）
- 画像挿入は `\usepackage[dvipdfmx]{graphicx}`
- tgif図は `tgifs/` フォルダ、gnuplot図は `gnuplots/` フォルダに置く
- 図の位置指定は `[H]`（here パッケージ）または `[htbp]`
- サブキャプションは `subcaption` パッケージ + `minipage` で並べる
- 表の罫線は `booktabs` の `\toprule`, `\midrule`, `\bottomrule` を使う
- アルゴリズムは `\usepackage[lined,linesnumbered,boxed]{algorithm2e}`
- アルゴリズム名は日本語化する:
  ```
  \SetAlgorithmName{アルゴリズム}{アルゴリズム}{アルゴリズムのリスト}
  \SetKwInput{KwIn}{入力}
  \SetKwInput{KwOut}{出力}
  ```

## 参照・引用

- 図の参照: `図\ref{fig:xxx}`（「図」と `\ref` の間にスペースなし）
- 式の参照: `式\eqref{eq:xxx}`
- 表の参照: `表\ref{tab:xxx}`
- アルゴリズム参照: `アルゴリズム\ref{alg:xxx}`
- ラベル命名規則:
  - 図: `fig:` 、式: `eq:` 、表: `tab:` 、アルゴリズム: `alg:`

## 参考文献

- `thebibliography` 環境 + `\bibitem` で書く（BibTeXは使わない）
- 並び順はアルファベット順（著者の姓で）
- ラベル名は著者イニシャル+年（例: `AC11`）または著者名+年（例: `pardalos1999`）

### 論文

```
著者名: タイトル. {\it 雑誌名} {\bf 巻} (年) ページ.
```

例:
```
\bibitem{AC11}
N. Ailon and M. Charikar: Fitting tree metrics: hierarchical
clustering and phylogeny.
{\it SIAM Journal on Computing} {\bf 40} (2011) 1275--1291.
```

### 書籍

```
著者名: \textit{書名} (出版社, 年).
```

例:
```
\bibitem{semple2033}
C. Semple and M. Steel: \textit{Phylogenetics}
(Oxford University Press, 2003).
```

### 修士論文・卒業論文

```
著者名: タイトル. 修士論文. 大学名, 年月.
```

例:
```
\bibitem{ishida25}
石田京太郎: 重み付き$\ell_1$最良近似超距離木問題に対する
部分木交換操作に基づく局所探索アルゴリズム.
修士論文. 静岡大学大学院総合科学技術研究科, 2025年2月.
```

### 書式の共通ルール

- 雑誌名はイタリック体: `{\it 雑誌名}` または `\textit{雑誌名}`
- 巻番号は太字: `{\bf 巻}` または `\textbf{巻}`
- ページ範囲はenダッシュ: `211--222`（ハイフン2つ）
- 著者の区切りは `and`（3人以上でも全員記載）
- 著者とタイトルの間はコロン + スペース

## 文体・構成

- 「である・だ」調を使う（敬体は使わない）
- `\par` で明示的に段落を区切ることが多い
- 初出の用語は `\textbf{}` で太字にする
- 定理・補題・命題・定義は `\newtheorem` で定義して使う

## コンパイル

```
ptex2pdf -l ファイル名.tex
```

参照がある場合は2回実行する。

## 文書ごとの設定

| | 報告書 | アブストラクト | 卒論 | ゼミ本体 |
|---|---|---|---|---|
| クラス | `jsarticle` | `jarticle` | `jreport` | `jarticle` |
| スタイル | なし | `chukan.sty` | `systhesisu.sty` | なし |
| 構造 | `\section` | `\section` | `\chapter` | `\section` |
| 段組 | 1段 | 2段 | 1段 | 1段 |
| フォントサイズ | 指定なし | 9pt | 11pt | 11pt |
