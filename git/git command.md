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
        mf = "!f(){ git commit -m \":sparkles: ${1}\"; };f"
        mr = "!f(){ git commit -m \":recycle: ${1}\"; };f"
        mt = "!f(){ git commit -m \":white_check_mark: ${1}\"; };f"
        ma = "!f(){ git commit -m \":art: ${1}\"; };f"
        mar = "!f(){ git commit -m \":building_construction: ${1}\"; };f"
        md = "!f(){ git commit -m \":memo: ${1}\"; };f"
    ```
    
    mf: commit feature
    
    mr: commit refactor

    mt: commit test

    ma: commit styles

    mar: commit architectural

    md: commit document