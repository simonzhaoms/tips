# YAML #

[YAML (YAML Ain't Markup Language)](https://yaml.org/) is an
indentation-based file format for data serialization.  A JSON
(JavaScript Object Notation) doc can be easily converted to a YAML
doc, since JSON is a subset of YAML.

**NOTE**: Only spaces is allowed for indentation, not tabs.


## YAML Syntax ##

### Dictionary ###

<table>
<tr><th>YAML</th><th>JSON</th></tr>
<tr>
  <td>
  
```yaml
number: 3.14159
bool: true
string: 'hello'
another string: bye bye
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
  "another string": "bye bye",
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


### List ###

<table>
<tr><th>YAML</th><th>JSON</th></tr>
<tr>
  <td>

```yaml
list:
  - apple
  - pear
  - orange
another_list: [apple, pear, orange]
list-of-dict:
  - name: Simon
    weight: 66
  - surname: Zhao
```
  </td>
  <td>

```json
{
  "list": [
    "apple",
    "pear",
    "orange"
  ],
  "another_list": [
    "apple",
    "pear",
    "orange"
  ],
  "list-of-dict": [
    {
      "name": "Simon",
      "weight": 66
    },
    "surname": "Zhao"
  ]
}
```
  </td>
</tr>
</table>


### Multiple-lines value ###

<table>
<tr><th>YAML</th><th>JSON</th></tr>
<tr>
  <td>

```yaml
code: |
  if args.version:
      print(version)
```
  </td>
  <td>

```json
{
  "code": "if args.version:\n    print(version)\n"
}
```
  </td>
</tr>
</table>


### Multiple documents in a single YAML file ###

<table>
<tr><th>YAML</th><th>JSON</th></tr>
<tr>
  <td>

```yaml
name: Simon
---
name: Zhao
```
  </td>
  <td>

```json
{"name": "Simon"}
{"name": "Zhao"}
```
  </td>
</tr>
</table>


## Use YAML in Python ##

The [**pyyaml**](https://pyyaml.org/) package can be used to deal with
YAML file:

```bash
pip install pyyaml
```

To read YAML file:

```python
import yaml

# read YAML file containing a single YAML document
with open('xxx.yaml') as f:
    print(yaml.load(f))

# read YAML file containing multiple YAML documents
with open('yyy.yaml') as f:
    for doc in yaml.load_all(f)
        print(doc)

# read YAML file and keep the order of keys as well.
# the returned object is an OrderedDict
import yamlordereddictloader  # pip install yamlordereddictloader
with open('xxx.yaml') as f:
    print(yaml.load(f, Loader=yamlordereddictloader.Loader))
```

To convert Python data structure to YAML format:

```python
import yaml

one = {'name': 'Simon', 'weight': 66}
two = [one, one]

# dump one object
print(yaml.dump(one))

# dump multiple objects
print(yaml.dump_all(two))
```


## Reference ##

* [YAML](https://yaml.org/)
* [PyYAML](https://pyyaml.org/)
    + [PyYAML Documentation](https://pyyaml.org/wiki/PyYAMLDocumentation)
    + [PyYAML GitHub](https://github.com/yaml/pyyaml/)
* [YAML Tutorial](https://gettaurus.org/docs/YAMLTutorial/)
* [YAML ain't Markup Language | Completely Different](http://jessenoller.com/blog/2009/04/13/yaml-aint-markup-language-completely-different)
* [How to read YAML file in Python with ordered keys](https://codeyarns.com/2017/11/23/how-to-read-yaml-file-in-python-with-ordered-keys/)
