# Editor config

One of the biggest issue we have in cooperation is to keep the same coding style in developing.

In our team, different people use different IDE. For example, 2 FE developers use `Vs code` because they focus on Typescript and I use `IDEA` as I need to work on Typescript, Python and Java. Thus, to keep all the teammates same coding style is necessary.&#x20;

Currently, most of the IDE support `EditorConfig`  and what we need to do is adding a `.editorconfig` file at the root of your project.

For most of the project the configure is:

```
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
indent_size = 4

[*.{js, jsx, css, scss, html, ts, tsx, py, json, xml}]
indent_style = space

```

more details check:

[https://editorconfig.org/](https://editorconfig.org/)
