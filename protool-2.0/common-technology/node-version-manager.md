# Node version manager

Node js is developing so quick that when I first work on the bolt project. It was 4 in rui. But now for protool it is 16.  So it is very common to have several node version on your computer.

### Install

To install the NVM by:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

After running the command above, the profile setting would also be written like:

```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

which loads the nvm automatically.

### How to use

One of the great benefit to install nvm is you don't need to go to node.js website to download the node engine independently,  what you need to do is just:

```bash
nvm install 16
```

After install complete, you can check it by:

```bash
node -v
v16.10.0
```

switch to another version:

```
nvm use 10
Now using node v10.16.0 (npm v6.9.0)
```

list all the version in your computer:

```bash
nvm ls
       v6.11.2
->     v10.16.0
       v12.18.3
       v16.8.0
       v16.10.0
         system
default -> 16 (-> v16.10.0)
node -> stable (-> v16.10.0) (default)
stable -> 16.10 (-> v16.10.0) (default)
iojs -> N/A (default)
unstable -> N/A (default)
lts/* -> lts/fermium (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.6 (-> N/A)
lts/fermium -> v14.17.6 (-> N/A)
```

To set the default version of node:

```bash
nvm alias default 10
default -> 10 (-> v10.16.0)
```





