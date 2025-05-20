---
layout: post
title: Jekyll ブログデプロイを Custom GitHub Actions Workflows に切り替えた
tags:
- jekyll
- GitHub Page
- チラシの裏
date: '2025-04-14T01:10:39+09:00'
last_modified_at: '2025-05-21T01:07:31+09:00'
---
これまで、GitHub Pagesではソースコードだけでなく、ビルド成果物もリポジトリで管理する必要があった。そのため、CIプロセスを利用してビルドを行い、ソースコードとは別のGitHub Pages用のリポジトリにプッシュする方法を採用していた。

[JekyllブログのTravis CIを使ってGitHub Pagesへのデプロイ方法についてのメモ]({% post_url 2015-04-30-jekyll-travis-ci-github-pages-deployment %})でも触れたように、2015年の本ブログへの導入当初はTravis CIを使用していたが、[2020年にはGitHub Actionsに移行](https://github.com/cat-in-136/cat-in-136.github.io/pull/9)した。ただし、このデプロイ手順自体は変更していなかった。

そして、2024年にはGitHub Actionsを使用して直接GitHub Pagesにデプロイできるようになった。これにより、プロセスがさらに簡素化され、効率的な運用が可能となった。

- [カスタムワークフローで GitHub Pages デプロイが可能に \| 豆蔵デベロッパーサイト](https://developer.mamezou-tech.com/blogs/2022/09/08/github-pages-new-deploy-method/)
- [GitHub Pages with Custom GitHub Actions Workflows are now generally available \- GitHub Changelog](https://github.blog/changelog/2024-03-25-github-pages-with-custom-github-actions-workflows-are-now-generally-available/)

やっと対応することにした。

これまで、cat-in-136/blog でソースを管理し、コミット時の GitHub Action でブログをビルドし、デプロイとして別レポジトリ cat-in-136/cat-in-136.github.io にコミットしていた。

レポジトリ名は以下のように変更する。

|元レポジトリ名                 |新レポジトリ名                        |備考    |
|-------------------------------|--------------------------------------|--------|
|cat-in-136/blog                |cat-in-136/cat-in-136.github.io       |        |
|cat-in-136/cat-in-136.github.io|cat-in-136/cat-in-136.github.io-backup|廃棄予定|

既存のレポジトリのまま変更するのではなく改名したのは、過去の情報を引き継ぐためである。レポジトリに紐付けられたSlack通知の設定はもちろん、レポジトリをwatchしている人の設定もそのまま引き継がれる。さらに、過去のリンクもある程度リダイレクトしてくれているようだ。非常に良い。

あとは GitHub のマニュアル通りに書き換える。レポジトリの設定 General -> Pages -> Build and deployment -> Source の設定を "GitHub Action" に変更した後は、単純にGitHub Workflowのデプロイ処理だけを変更すればよかった。

- [Using custom workflows with GitHub Pages \- GitHub Docs](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)

GitHub Workflow の意味のある部分を抜き出すと以下の通りである。

```yaml
jobs:
  build:
    steps:

    - # 中略

    - name: Generate document
      run: bundle exec rake generate

    - name: Upload artifact
      # Automatically uploads an artifact from the './_site' directory by default
      uses: actions/upload-pages-artifact@v3

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build

    steps:
    - name: Deploy to GitHub Pages
      id: deployment
      uses: actions/deploy-pages@v4
```

単に actions/deploy-pages@v4 を呼べば良い。ただ、お作法的に deploy と build を分けるのが好ましいようなので、ジョブを分けた。

不要になった cat-in-136/cat-in-136.github.io-backup はひとまずアーカイブにし、しばらくしたら削除する予定である。
