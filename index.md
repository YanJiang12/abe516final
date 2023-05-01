---
layout: default
---


# Introduction

  This is the transgenic crop value data in each states from the year 2000 to 2022. It discribe the corn, soybean, upland cotton by deviding them into categories as all GE varieties, Herbicide-tolerant, insect resistance, stacked gene varieties.
  
  The question on this dataset is how could we know the advantage and disadvantages of each states for planting the crops . Also, can we predict the future biotech development direction?

  At first, I tried to look at the table by myself. But it is full of numbers without any relationship. So  I decided  to use python help me resampling statistic and using machine learning to figure out how are they connected.

* * *
# Reform
*   1.Reform the table by different States

*   2.Reform the table by different Attributes

* * *

# Analysis

```python
#<Figure size 1400x1200 with 0 Axes>
import os.path
import pandas as pd
from matplotlib import pyplot as plt
plt.rcParams['font.sans-serif']=["SimHei"]
plt.figure(figsize=(14, 12))
# data1 = pd.read_csv("Biotech.csv")
data1 = pd.read_csv("BiotechCropsAllTables2022.csv")
data1['Value'] = data1["Value"].apply(lambda x: 0 if x =="*" or x=="." else int(x))

```

```python
# Setting up autolabel and year
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
```

* * *

```
# Analysis by States
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
    plt.savefig(f'State Analysis/{state}.jpg')
    plt.show()
```

![2668740f467d4b3969303a8243163b2](https://user-images.githubusercontent.com/130382954/235253790-972935ec-ec02-43f1-b4fc-f1e46bba21cd.png)

```
# State Average Value
dict1 = {k: v for k, v in sorted(dict1.items(), key=lambda item: item[1])}
cm1 = plt.bar([i for i in dict1.keys()],[i for i in dict1.values()],width=0.5,color="g")
autolabel(cm1)
plt.xlabel("State", size=12)
plt.ylabel("Value", size=12)
plt.xticks(rotation=-70)
plt.title("Average Value of each State ")
plt.tight_layout()
plt.legend()
plt.savefig(f'State Analysis/State Value trend.jpg')
plt.show()
```
![State Value trend](https://user-images.githubusercontent.com/130382954/235270266-f9d59094-094c-4e36-84ee-d78e8ae0bb85.jpg)

* * *
```
# Analysis by Attributes
for attribute in sorted(data1.Attribute.unique()):
    data2 = data1[data1["Attribute"] == attribute]
    mean2 = data2.Value.mean()
    dict2[attribute] = mean2
    plt.figure(figsize=(12, 8))
    for state in data2.State.unique():
        year_dict2 = {i: 0 for i in year1}
        data3 = data2[data2["State"] == state]
        for m in range(data3.shape[0]):
            year_dict2[list(data3["Year"])[m]] = list(data3["Value"])[m]
        plt.plot(year1, year_dict2.values(), marker='o', label=state)
    plt.xticks(fontproperties='Times New Roman', fontsize=10)
    plt.yticks(fontproperties='Times New Roman', fontsize=10)
    plt.title(f'Trend of {attribute}in each State')
    plt.legend()
    plt.savefig(f'Attribute Analysis/{attribute}.jpg')
    plt.show()
```
![All GE varieties (percent of all corn planted)](https://user-images.githubusercontent.com/130382954/235270338-ab5943a3-655e-43fb-acf1-0c179578dfe8.jpg)

```
# Attribute Average Value
dict2 = {k.replace(' (percent','(percent\n'): v for k, v in sorted(dict2.items(), key=lambda item: item[1],reverse=True)}
cm2 = plt.bar([i for i in dict2.keys()],[i for i in dict2.values()],width=0.5,color="r")
autolabel(cm2)
plt.xlabel("Attribute", size=12)
plt.ylabel("Value", size=12)
plt.title("Attribute Average score")
plt.xticks(rotation=90, ha='center')
plt.subplots_adjust(bottom=0.6)
plt.savefig(f'Attribute Analysis/Attribute.jpg')
plt.show()
```
![Attribute](https://user-images.githubusercontent.com/130382954/235270355-1988f8ad-eeee-4d86-b0b0-0fd74124f65b.jpg)

Project describes integration of class concepts and discusses why analysis was chosen
1.graph
2.feature selection
3.custer plots
* * *
# Reflection 

According to the analysis on states, Mississippi gets the highest average value as 62 points. It indicates this state is the best place of growing the biotech crop during the year 2000 to 2022.


- By each states:
  - ALabama: Stacked gene of upland cotton
  - Arkansas： All GE of upland cotton
  - Califonia：All GE of upland cotton
  - Georgia： Stacked gene of upland cotton
  - Illinois： Herbicide-tolerant of all soybeans,
  - Indiana： Herbicide-tolerant of all soybeans
  - Iowa： Herbicide-tolerant of soybeans
  - Kansas： Herbicide-tolerant of soybeans
  - Louisiana： Stacked gene of upland cotton
  - Mississippi： Herbicide-tolerant of soybeans
  - Missouri： All GE of upland cotton
  - Nebraska ： Herbicide-tolerant of soybeans
  - North Carolina：Stacked gene of upland cotton
  - North Dakota： Herbicide-tolerant of soybeans
  - Ohio： Herbicide-tolerant of soybeans
  - South Dakota：herbicide-tolerant of soybeans
  - Tenessee：Stacked gene of upland cotton
  - Texas：all GE of upland cotton
  - Wisconsin：Herbicide-tolerant of soybean

According to the analysis on attributes, the herbicide-tolerant soybean have the highest average score as 88 points. It means these two kinds soybean has the best growth during the year 2000 to 2022. 

- By each attributes
  - All GE of corn planted: Missouri
  - All GE of soybean: Mississippi
  - All GE of upland cotton: Tenessee
  - Herbicide-tolerant of corn: North Dakota
  - Herbicide-tolerant of soybean: Mississippi
  - Herbicide-tolerant of upland cotton: Missouri
  - Insect-resistant of corn: Texas
  - Insect-resistant of soybean: California
  - Insect-resistant of upland cotton:Illinois

* * *

# Methods

*   The machine learning is the major method used in the project, including the resampling statistics, Linear Regression, etc.

*   Machine learning is a subfield of artificial intelligence that  enable computer systems to automatically learn and improve from experience without being explicitly programmed. Its limitations include the potential for biased results, overfitting, and the need for large amounts of high-quality data. Despite these limitations, machine learning can be useful for research projects because it can uncover patterns and relationships in data that might not be immediately apparent to human analysts, enabling researchers to make more accurate predictions and identify new insights that can drive further research.

*   Advantage:
1.Easy to learn and use: Machine learning can be easily used in Python for analysisng data.

2.Large selection of libraries and tools: I can directly input the file with large amount data.

*   Disadvantage:

Performance: It can not work well with complex dateset and it requirs the user to control the form of the dataset.

There is no requirement for the transformation for the dataset. The python language can handle  it automatically.
* * *

# Discussion

My dataset file is free to access from the USDA website. Feel free to use:

https://www.ers.usda.gov/data-products/adoption-of-genetically-engineered-crops-in-the-u-s/

It is fully findable, accessible, reusable and available. Also I put the files, both the datas and results, in the github for reproducing this analysis. 

Learning the regularity of the recorded can help figuring out the advantage and disadvantages of each states for planting the crops and predicting the future biotech development direction.
* * *

# Assignment 

Please present the analysis by boxplot table.  



