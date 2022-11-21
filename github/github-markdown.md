# GitHub Markdown #


* [Souce code color highlighting](#souce-code-color-highlighting)
* [Table](#table)
* [How to fold/collapse a setion](#how-to-foldcollapse-a-setion)
* [Align images/pictures](#align-imagespictures)
* [LaTeX math equation](#latex-math-equation)
* [Reference](#reference)


## Souce code color highlighting ##

See:
- [Creating and highlighting code blocks](https://help.github.com/articles/creating-and-highlighting-code-blocks/)
- [List of supported languages on GitHub](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)
- [How to escape backticks in code block ?](https://github.com/jonschlinkert/remarkable/issues/146)

<details>
<summary>Click to see more ...</summary>

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


### Escape backticks ###

Use more backticks instead of only 3 backticks to escape backticks
inside code block:

``````
````
Some code

```
Some code inside another code
```
````
``````

````
Some code

```
Some code inside another code
```
````

</details>


## Table ##

See:
- [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
- [Organizing information with tables](https://help.github.com/articles/organizing-information-with-tables/)
- [Github markdown, syntax highlight of code blocks in the table cell](https://stackoverflow.com/a/53038904)

<details>
<summary>Click to see more ...</summary>

### What GitHub Markdown can do ###

**NOTE**: Blank/empty cells should use `&nbsp;`, otherwise they will
not be rendered correctly.

```Markdown
header 1 | header 2 | center | left aligned | right aligned
-------- | -------- | :----: | :----------- | ------------:
r 1 c 1 | r 1 c 2 | r 1 c 3 blablabla | r 1 c 4 blablabla | r 1 c 5 blablabla
&nbsp;  | r 2 c 2 | r 2 c 3 | r 2 c 4 | r 2 c 5
r 3 c 1 | r 3 c 2 | r 3 c 3 | r 3 c 4 | r 3 c 5
```

header 1 | header 2 | center | left aligned | right aligned
-------- | -------- | :----: | :----------- | ------------:
r 1 c 1 | r 1 c 2 | r 1 c 3 blablabla | r 1 c 4 blablabla | r 1 c 5 blablabla
&nbsp;  | r 2 c 2 | r 2 c 3 | r 2 c 4 | r 2 c 5
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

To put code blocks inside a table cell, add a blank line before the
markdown code block:

``````html
<table>
<tr><th>YAML</th><th>JSON</th></tr>
<tr>
  <td>
  
```yaml
number: 3.14159
bool: true
string: 'hello'
another-string: bye bye
dict:
  name: Simon
  weight: 66
another-dict: {name: Simon, weight: 66}
```
  </td>
  <td>

```json
{
  "number": 3.14159,
  "bool": true,
  "string": "hello",
  "another-string": "bye bye",
  "dict": {
    "name": "Simon",
    "weight": 66
  },
  "another-dict": {
    "name": "Simon",
    "weight": 66
  }
}
```
  </td>
</tr>
</table>
``````

<table>
<tr><th>YAML</th><th>JSON</th></tr>
<tr>
  <td>
  
```yaml
number: 3.14159
bool: true
string: 'hello'
another-string: bye bye
dict:
  name: Simon
  weight: 66
another-dict: {name: Simon, weight: 66}
```
  </td>
  <td>

```json
{
  "number": 3.14159,
  "bool": true,
  "string": "hello",
  "another-string": "bye bye",
  "dict": {
    "name": "Simon",
    "weight": 66
  },
  "another-dict": {
    "name": "Simon",
    "weight": 66
  }
}
```
  </td>
</tr>
</table>

</details>


## How to fold/collapse a setionp ##

This can be done by using HTML since it is not directly supported by
GitHub Markdown.

See:
- [A collapsible section with markdown](https://gist.github.com/pierrejoubert73/902cc94d79424356a8d20be2b382e1ab)

<details>
<summary>Click to see more ...</summary>

```
<details>
<summary>Click here ...</summary>

This sentence will be collapsed/expanded by clicking the line above.

</details>
```

<details>
<summary>Click here ...</summary>

This sentence will be collapsed/expanded by clicking the line above.

</details>

</details>


## Align images/pictures ##

To show a single picture in a GitHub markdown file, one can use
`![alternative text](URL)`.  But aligning pictures can be done by
using HTML since it is not directly supported by GitHub Markdown.

See:
- [Center alignment](https://stackoverflow.com/a/51992125)
- [Left and right alignment](https://stackoverflow.com/a/50192235)

<details>
<summary>Click to see more ...</summary>

### Center alignment ###

```html
<p align="center"> 
  <img src="put image url here" alt="alternate text">
</p>
```

### Left Alignment ###

```html
<img align="left" src="put image url here">
```

### Right Alignment ###

```html
<img align="right" src="put image url here">
```

### Side by Side ###

The most important is to adjust the `height` or `width` of the
pictures to let them fit into a row.

```html
<img align="center" src="url 1" height="250"/>
<img align="center" src="url 2" height="250"/>
```

</details>


## LaTeX math equation ##

<details>
<summary>Click to see more ...</summary>

This can be done by using the service from [CodeCogs
Equation](http://latex.codecogs.com/).  You can put the LaTeX math
equation as parameter to the end of
`http://latex.codecogs.com/svg.latex?`, then a svg image of the
equation will be generated so that you can put the composed link as
embedded image in Markdown doc.  For example, to display LeTaX
equation `\frac{1}{1+sin(x)}`, you can use

```markdown
![my equation](http://latex.codecogs.com/svg.latex?\frac{1}{1+sin(x)})
```

Then it will be shown as a image looks like ![my
equation](http://latex.codecogs.com/svg.latex?\frac{1}{1+sin(x)}).

### Update on 21/11/2022 ###

As announced in 19/05/2022 at [Math support in
Markdown](https://github.blog/2022-05-19-math-support-in-markdown/),
GitHub now supports math expressions natively in Markdown by using the
JavaScript library MathJax.  See [Writing mathematical expressions:
Use Markdown to display mathematical expressions on
GitHub](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions).

Available TeX/LaTeX commands are listed in [Supported TeX/LaTeX
commands](https://docs.mathjax.org/en/latest/input/tex/macros/index.html).
For example, if the following LaTex math equation is put inside a
`` ```math `` code block:

```latex
\mathbf{J} = [
  \frac{\partial\mathbf{Y}}{\partial x_1},
  \frac{\partial\mathbf{Y}}{\partial x_2},
  \ldots,
  \frac{\partial\mathbf{Y}}{\partial x_n}
  ] =
  \begin{bmatrix}
    \frac{\partial f_1}{\partial x_1} & \cdots &\frac{\partial f_1}{\partial x_n} \\
    \vdots                            & \ddots & \vdots  \\
    \frac{\partial f_m}{\partial x_1} & \cdots & \frac{\partial f_m}{\partial x_n}
  \end{bmatrix}
```

then it will be rendered by GitHub as:

```math
\mathbf{J} = [
  \frac{\partial\mathbf{Y}}{\partial x_1},
  \frac{\partial\mathbf{Y}}{\partial x_2},
  \ldots,
  \frac{\partial\mathbf{Y}}{\partial x_n}
  ] =
  \begin{bmatrix}
    \frac{\partial f_1}{\partial x_1} & \cdots &\frac{\partial f_1}{\partial x_n} \\
    \vdots                            & \ddots & \vdots  \\
    \frac{\partial f_m}{\partial x_1} & \cdots & \frac{\partial f_m}{\partial x_n}
  \end{bmatrix}
```


</details>


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


