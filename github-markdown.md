# GitHub Markdown #


* [Table](#table)
* [Reference](#reference)


## Table ##

See:
- [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
- [Organizing information with tables](https://help.github.com/articles/organizing-information-with-tables/)


### What GitHub Markdown can do ###

```
header 1 | header 2 | header 3 | left aligned | right aligned
-------- | -------- | -------- | :----------- | ------------:
row 1 column 1 | row 1 column 2 | row 1 column 3 | row 1 column 4 | row 1 column 5
row 2 column 1 | row 2 column 2 | row 2 column 3 | row 2 column 4 | row 2 column 5
row 3 column 1 | row 3 column 2 | row 3 column 3 | row 3 column 4 | row 3 column 5
```

header 1 | header 2 | header 3 | left aligned | right aligned
-------- | -------- | -------- | :----------- | ------------:
row 1 column 1 | row 1 column 2 | row 1 column 3 | row 1 column 4 | row 1 column 5
row 2 column 1 | row 2 column 2 | row 2 column 3 | row 2 column 4 | row 2 column 5
row 3 column 1 | row 3 column 2 | row 3 column 3 | row 3 column 4 | row 3 column 5


### What can only be done by HTML ###

```
<table>
<thead><tr><th>header 1</th><th>header 2</th><th>header 3</th></tr></thead>
<tbody>
<tr><td>row 1 column 1</td><td style="text-align:right">row 1 column 2</td><td rowspan="2">row 1-2 column 3</td></tr>
<tr><td>row 2 column 1</td><td style="text-align:right">row 2 column 2</td>                                     </tr>
<tr><td colspan="3">row 3 column 1-3</td></tr>
</tbody>
</table>
```

<table>
<thead><tr><th>header 1</th><th>header 2</th><th>header 3</th></tr></thead>
<tbody>
<tr><td>row 1 column 1</td><td style="text-align:right">row 1 column 2</td><td rowspan="2">row 1-2 column 3</td></tr>
<tr><td>row 2 column 1</td><td style="text-align:right">row 2 column 2</td>                                     </tr>
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


