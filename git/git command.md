# Git command



## git command setting

1. set default editor

```shell
git config --global core.editor code
```

2. edit the git config globally

```shell
git config --edit --global
```

3. create branch


```gitconfig
[alias]
    cb = "!sh -c \"set -ex; git checkout -b $1; git push origin $1; git push -u origin $1\""
```


4. delete branch

```gitconfig
[alias]
    db = "!sh -c \"set -ex; git branch -d $1; git push origin :$1\""
```

5. pull all

```gitconfig
[alias]
    px = "!sh -c \"set -ex; git pull --prune; git fetch --tags --prune\""
```

6. commit command


    6.1 normal commit

    ```
    [alias]
        cm = commit -m
    ```

    6.2 commit with gitmoji
    <https://gitmoji.dev/>


    ```
    [alias]
        cr = "!sh -c \"set -ex; git commit -m $1; git push origin :$1\""
    ```