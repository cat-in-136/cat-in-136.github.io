---
layout: post
title: Redmine Hearts の終息
tags:
- redmine
- チラシの裏
thumbnail: "{% asset_image_path 2025-09-28-heart-and-reaction.png %}"
date: '2025-09-28T08:30:18+09:00'
---

<figure>
{% asset_image_tag fitcontain 2025-09-28-heart-and-reaction.png %}
<figcaption>Redmine 6.1 でRedmine Hearts と Redmine リアクションの2種類のいいねが表示される状態</figcaption>
</figure>

[cat-in-136/redmine_hearts](https://github.com/cat-in-136/redmine_hearts) を Redmine 6.1 でのリアクション機能（「いいね」機能）導入 ( [Feature #42630: Introduce reaction feature to issues, notes, news, and forums](https://www.redmine.org/issues/42630) ) に伴って、開発を終了することとした。これに伴い、[リアクションへの変換タスクを追加した](https://github.com/cat-in-136/redmine_hearts/pull/60)。今まで使っていた人は、Redmine 6.1 に上げると Redmine Hearts と Redmine リアクションの2種類のいいねが表示される状態になるので、変換タスク `redmine_hearts:migrate_to_reactions` で変換したらアンインストールしてほしい。

> ### <span style="color:red;background-color:yellow;">End of Life and Migration to Redmine 6.1+ Reactions</span>
>
> Redmine Hearts will not be updated for Redmine versions 6.1 and above, as Redmine 6.1 introduces a built-in reaction feature.  
> It is recommended to migrate to the built-in reaction feature if you are using Redmine 6.1 or newer.
>
> The latest version of Redmine Hearts includes a migration task for this purpose.
> After upgrading to Redmine v6.1, migrate to the reaction feature by following the steps [outlined in the README.rdoc](https://github.com/cat-in-136/redmine_hearts/blob/master/README.rdoc#label-End+of+Life+and+Migration+to+Redmine+6.1-2B+Reactions).
> Once migration is complete, you can remove this plugin.
>
> --- [redmine_hearts - Plugins - Redmine](https://www.redmine.org/plugins/redmine_hearts)


もともとこの「いいね！」のプラグインは、 [サイボウズLiveからredmineへの移行]({% post_url  2019-01-26-migrate-cybozu-live-to-redmine-forum %})で言及した通り、サイボウズLiveからの移植の経緯で開発した。

> Redmine にいいね!の機能は存在しない。そのためプラグインを入れることになるが、フォーラムにいいね!できるのは見当たらなかった。そこで下記の通り自作した。
>
> [cat-in-136/redmine_hearts](https://github.com/cat-in-136/redmine_hearts)

それが [Ruby Issue Tracking System の Redmine](https://bugs.ruby-lang.org/) にもインストールされたのは感慨深かった。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr"><a href="https://t.co/EdvcUUdCRb">https://t.co/EdvcUUdCRb</a> にいいね！が追加されている👍 <a href="https://t.co/erHqdyJOyd">https://t.co/erHqdyJOyd</a> <a href="https://t.co/ANWtzq2O3k">https://t.co/ANWtzq2O3k</a> <a href="https://t.co/ZtBBW3MFDC">pic.twitter.com/ZtBBW3MFDC</a></p>&mdash; cat_in_136 (@cat_in_136) <a href="https://twitter.com/cat_in_136/status/1873892693857956140?ref_src=twsrc%5Etfw">December 31, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

ここのいいねがきちんとリアクションに移行されるのを心待ちにして待つこととしよう
