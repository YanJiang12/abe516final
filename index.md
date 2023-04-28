---
layout: default
---

Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](./another-page.html).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# Introduction

  This is the transgenic crop value data in each states from the year 2000 to 2022. It discribe the corn, soybean, upland cotton by deviding them into categories as all GE varieties, Herbicide-tolerant, insect resistance, stacked gene varieties.
  
  Studying this data table can be helpful on figuring out the advantage and disadvantages of each states for planting the crops and predicting the future biotech development direction.

* * *
# Reform
*   1.Reform the table by different States

*   2.Reform the table by different Attributes

* * *

# Analysis

```python
import os.path
import pandas as pd
from matplotlib import pyplot as plt
plt.rcParams['font.sans-serif']=["SimHei"]
plt.figure(figsize=(14, 12))
data1 = pd.read_csv("BiotechCropsAllTables2022.csv")
data1['Value'] = data1["Value"].apply(lambda x: 0 if x =="*" or x=="." else int(x))
def autolabel(rects):
    for rect in rects:
        height = rect.get_height()
        plt.text(rect.get_x()+rect.get_width()/2.-0.08, 1.03*height, '%s' % int(height), size=10, family="Times new roman")

dict1 = {}
dict2 = {}

year1 = sorted(data1.Year.unique())

if not os.path.exists("State Analysis"):
    os.makedirs("State Analysis")
if not os.path.exists("Attribute Analysis"):
    os.makedirs("Attribute Analysis")
for state in sorted(data1.State.unique()):
    data2 = data1[data1["State"] == state]
    mean1 = data2.Value.mean()
    dict1[state] = mean1

    plt.figure(figsize=(12, 8))
    for attribute in data2.Attribute.unique():
        year_dict1 = {i: 0 for i in year1}
        data3 = data2[data2["Attribute"]==attribute]
        for m in range(data3.shape[0]):
            year_dict1[list(data3["Year"])[m]] = list(data3["Value"])[m]
        plt.plot(year1, year_dict1.values(), marker='o', label=attribute.replace('percent','percent\n'))
    plt.xticks(fontproperties='Times New Roman', fontsize=10)
    plt.yticks(fontproperties='Times New Roman', fontsize=10)
    plt.title(f'The trend of each Attributes in {state}')
    plt.legend()
    plt.show()
    plt.savefig(f'State Analysis/{state}.jpg')

```
![2668740f467d4b3969303a8243163b2](https://user-images.githubusercontent.com/130382954/235253790-972935ec-ec02-43f1-b4fc-f1e46bba21cd.png)

Project describes integration of class concepts and discusses why analysis was chosen
1.graph
2.feature selection
3.custer plots
* * *
# Reflection 
comparison on features
ability to product yields
what data is useful/missing
* * *

# Methods
what from the class did you use in this project and why might it be useful for research projects like this?
What are the advantages and disadvantages?  
Were there any assumptions or transformations needed? 

*   The machine learning is the major method used in the project.

*   Machine learning is a subfield of artificial intelligence that  enable computer systems to automatically learn and improve from experience without being explicitly programmed. Its limitations include the potential for biased results, overfitting, and the need for large amounts of high-quality data. Despite these limitations, machine learning can be useful for research projects because it can uncover patterns and relationships in data that might not be immediately apparent to human analysts, enabling researchers to make more accurate predictions and identify new insights that can drive further research.

*   Advantage:
1.Easy to learn and use: Machine learning can be easily used in Python for analysisng data.

2.Large selection of libraries and tools: I can directly input the file with large amount data.

*   Disadvantage:

Performance: It can not work well with complex dateset and it requirs the user to control the form of the dataset.

There is no requirement for the transformation for the dataset. The python language can handle  it automatically.
* * *

# Discussion
How much does your analysis attain the FAIR principles? For example, what is the ability to automate and reproduce your analysis (if the file input were to change, could this analysis be reproduced and how easily?)  - how will someone else reproduce this analysis?  Is the data stored somewhere?  Can I reproduce the figures easily?
Creation of one assignment based on your dataset for the class to complete - one can think of this of a task or homework assignment based on your project.


```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6


### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)



### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
