# GitHub Markdown #


* [Souce code color highlighting](#souce-code-color-highlighting)
* [Table](#table)
* [Reference](#reference)


## Souce code color highlighting ##

See:
- [Creating and highlighting code blocks](https://help.github.com/articles/creating-and-highlighting-code-blocks/)
- [github/linguist/lib/linguist/languages.yml](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)


### Console code ###

<pre lang="no-highlight"><code>
```console
$ pip3 install mlhub
Collecting mlhub
  Downloading https://files.pythonhosted.org/packages/61/4c/0fe1b263358bad88525594a8dd319c40934c16e6c3cc01f32b0b8edb5537/mlhub-2.0.1.tar.gz
Collecting pyyaml (from mlhub)
...
$ ml --version
mlhub version 2.0.1
```
</code></pre>

```console
$ pip3 install mlhub
Collecting mlhub
  Downloading https://files.pythonhosted.org/packages/61/4c/0fe1b263358bad88525594a8dd319c40934c16e6c3cc01f32b0b8edb5537/mlhub-2.0.1.tar.gz
Collecting pyyaml (from mlhub)
...
$ ml --version
mlhub version 2.0.1
```

### C++ ###

<pre lang="no-highlight"><code>
```c++
#include<iostream>

int main() {
  std::cout << "Hello World!\n";
  return 0;
}
```
</code></pre>

```c++
#include<iostream>

int main() {
  std::cout << "Hello World!\n";
  return 0;
}
```

### No highlight ###

<pre lang="no-highlight"><code>
```no-highlight
# Header 1
## Header 2
### Header 3
```
</code></pre>

```no-highlight
# Header 1
## Header 2
### Header 3
```


## Table ##

See:
- [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
- [Organizing information with tables](https://help.github.com/articles/organizing-information-with-tables/)


### What GitHub Markdown can do ###

```Markdown
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


