# GitHub Markdown #


* [Table](#table)
* [Reference](#reference)


## Table ##

See:
- [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
- [Organizing information with tables](https://help.github.com/articles/organizing-information-with-tables/)


### What GitHub Markdown can do ###

```markdown
header 1 | header 2 | center | left aligned | right aligned
-------- | -------- | :----: | :----------- | ------------:
r 1 c 1 | r 1 c 2 | r 1 c 3 blablabla | r 1 c 4 blablabla | r 1 c 5 blablabla
r 2 c 1 | r 2 c 2 | r 2 c 3 | r 2 c 4 | r 2 c 5
r 3 c 1 | r 3 c 2 | r 3 c 3 | r 3 c 4 | r 3 c 5
```

header 1 | header 2 | center | left aligned | right aligned
-------- | -------- | :----: | :----------- | ------------:
r 1 c 1 | r 1 c 2 | r 1 c 3 blablabla | r 1 c 4 blablabla | r 1 c 5 blablabla
r 2 c 1 | r 2 c 2 | r 2 c 3 | r 2 c 4 | r 2 c 5
r 3 c 1 | r 3 c 2 | r 3 c 3 | r 3 c 4 | r 3 c 5


### What can only be done by HTML ###

```html
<table>
<thead><tr><th>header 1</th><th>header 2</th><th>header 3</th></tr></thead>
<tbody>
<tr><td>row 1 column 1</td><td align="right">row 1 column 2 blablabla</td><td rowspan="2">row 1-2 column 3</td></tr>
<tr><td>row 2 column 1</td><td align="right">row 2 column 2</td></tr>
<tr><td colspan="3">row 3 column 1-3</td></tr>
</tbody>
</table>
```

<table>
<thead><tr><th>header 1</th><th>header 2</th><th>header 3</th></tr></thead>
<tbody>
<tr><td>row 1 column 1</td><td align="right">row 1 column 2 blablabla</td><td rowspan="2">row 1-2 column 3</td></tr>
<tr><td>row 2 column 1</td><td align="right">row 2 column 2</td></tr>
<tr><td colspan="3">row 3 column 1-3</td></tr>
</tbody>
</table>


## Reference ##

### GitHub official reference ###

- [About writing and formatting on GitHub](https://help.github.com/articles/about-writing-and-formatting-on-github/)
- [Basic writing and formatting syntax](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
- [Mastering markdown](https://guides.github.com/features/mastering-markdown/)
- [GitHub flavored markdown spec](https://github.github.com/gfm/)
- [Autolinked references and URLs](https://help.github.com/articles/autolinked-references-and-urls/)


### Other reference ###

- [GitHub markdown reference](https://github.com/RickCogley/Github-Markdown-Reference)
- [Anchors in Markdown](https://gist.github.com/asabaylus/3071099)


