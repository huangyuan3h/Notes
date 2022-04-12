# Git ignore

As our developing is based on `git` as version control system. There are something we should not commit to the repository should be ignored in the `.gitignore` configure file.

Here is a simple example:

```
node_modules/

# remove coverage
coverage/

# IDE
.idea/
.vscode/

# schema
schema.gql

# typescript build
dist/

# yarn package manager
yarn.lock

# system file for mac
.DS_Store

# config file
.env

# log related file
logs/
```

The way we add configuration to this file is much more like find one and add one.

You may find in some project this file is based on the templates. For me it is not necessary.
