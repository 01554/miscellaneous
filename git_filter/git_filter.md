# Gitコミットログの名前を書き換える

使い始めたばかりのパソコンでgit.config忘れてたとか
会社のPCと家のPCの使い分けミスったとかの時に使うやつ

## 何も気にせず全部書き換える（自分だけが扱ってるリポジトリとか）

```
git filter-branch -f --env-filter   "GIT_AUTHOR_NAME='新しい名前'; \
GIT_AUTHOR_EMAIL='新しいアドレス'; \
GIT_COMMITTER_NAME='新しい名前'; \
GIT_COMMITTER_EMAIL='新しいアドレス';" HEAD


$ git log --pretty=full
$ git push -f

```



## 複数人で扱っていやつなので自分のやつだけ書き換える
```
$ git filter-branch -f --env-filter '
    if test "$GIT_AUTHOR_EMAIL" = "旧メアド(hoge@local など)"
    then
        GIT_AUTHOR_EMAIL="新メアド"
        GIT_AUTHOR_NAME="新しい名前"
    fi
    if test "$GIT_COMMITTER_EMAIL" = "旧メアド(hoge@local など)"
    then
        GIT_COMMITTER_EMAIL="新メアド"
        GIT_COMMITTER_NAME="新しい名前"
    fi' --tag-name-filter cat HEAD

$ git log --pretty=full
$ git push -f
```

