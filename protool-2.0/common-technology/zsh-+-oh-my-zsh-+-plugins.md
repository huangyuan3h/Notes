# Zsh + oh my zsh + plugins

### Zsh

[ZSH](https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH), also called the Z shell, is an extended version of the Bourne Shell (sh), with plenty of new features, and support for plugins and themes.  Plus, The last OS X upgrade made ZSH the default shell.&#x20;

So when you type the command below you should see:

```
echo "$SHELL"
/bin/zsh
```

If the result is not zsh you can do:

```bash
chsh -s $(which zsh)
```

to change it to zsh

### Theme

To have a nice theme could speed up you programming, it could highlight the important information for you and ignore the others.

`oh-my-zsh` is one of the most popular theme for zsh, installing it by:

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

It is also fine to choose the theme you like, it doesn't matter.

### Plugins

After you configure the zsh theme, it would be nice to choose some plugins for you zsh:

1. [Zsh Autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
2. [web search](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/web-search)







#### Reference:

****[**https://www.zsh.org/**](https://www.zsh.org/)****

****[**https://ohmyz.sh/**](https://ohmyz.sh/)****
