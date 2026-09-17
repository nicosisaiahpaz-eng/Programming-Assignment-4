# Programming-Assignment-4
#### Made by: Nicos Isaiah M. Paz | 2ECE-C
## Objectives:
At the end of this laboratory activity, the student should be able to:
1. filter tabular data using several categorical and numerical conditions;
2. construct focused DataFrames by selecting relevant features;
3. summarize the relationship between categorical features and a numerical variable; and
4. communicate a data comparison using clear and correctly labeled plots.

## A. Visayas Communication DataFrame
Create a DataFrame assigned as `VisComm` containing students whose `Hometown` is `Visayas` and `Track` is `Communication`. The information that must be retained and displaye must be: Name, `Gender, Math, Electronics, Average`

The DataFrame and its number of rows must be displayed.

* `import pandas as pd` - loads the pandas library into the code and is assigned as pd.
* `pd.read_excel` - loads an excel or .xlsx file into the python code.
*  `df['Average']=df[['Math', 'Electronics']].mean(axis=1)` - gets the mean of the columns inside the double bracket, while `axis=1` specifies that the average is taken from the row instead of the column.
*  `.shape[]` - states the number of rows and or columns specified inside the bracket as 0 or 1 respectively.

#### Code
```python
import pandas as pd

df = pd.read_excel('board2.xlsx')
df

df['Average']=df[['Math', 'Electronics']].mean(axis=1)
VisComm = df.loc[(df['Hometown']=='Visayas')&(df['Track']=='Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
VisComm

VisComm.shape[0]
```

## B. Visayas Female DataFrame
Create a second DataFrame assigned as `VisFemale` containing students whose `Hometown` is `Visayas` and `Gender` is `Female`. The information that must be retained and displayed are: `Name, Track, GEAS, Electronics, Average`

After displaying `VisFemale`, the code must also display the rows in which the `Average` is `at least 60`.

* `df['Average']=df[['GEAS', 'Electronics']].mean(axis=1)` - gets the mean of the columns GEAS and Electronics inside the double bracket, while specifying the average taken by row denoted by `axis=1`
* `VisFemale = df.loc[(df['Hometown']=='Visayas')&(df['Gender']=='Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]` - calls the rows that the Hometown is Visayas and Gender is Female while displaying the Name, Track, GEAS, Electronics and the average for both.
* `VisFemale60 = VisFemale.loc[(VisFemale['Average']>=60)]` - calls the Averages that are greater than or equal to 60.

#### Code
```python
df['Average']=df[['GEAS', 'Electronics']].mean(axis=1)

VisFemale = df.loc[(df['Hometown']=='Visayas')&(df['Gender']=='Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale

VisFemale60 = VisFemale.loc[(VisFemale['Average']>=60)]
VisFemale60
```

## C. Category-Average Visualization
In this problem, the code must display three summary tables of the Average of each categorical feature Track, Gender, and Hometown. Then must display a bar graph containing all three to be visually compared, with the observation for each category written below the graph.

* `df.groupby()[[]]` - calls the column that is needed to be separated inserted inside the parenthesis and the column name that needs to be calculated upon inside the double bracket using codes such as `mean()`.
* `mean()` - calculates the average of a certain column or group of columns.
* `reset_index()` - resets the index of the DataFrame to default integer index.
* `import matplotlib.pyplot as plt` - imports the matplotlib library into the code and assigned as plt.
* `plt.subplots(1, 3, figsize=(15, 5), sharey=True)` - creates 3 plots side by side that is 15in wide and 5in tall, while all sharing the same Y-axis.
* `axes[].bar()` - creates a bar chart with its location inside plt.subplot specified inside the brackets, and specifies the contents and features such as category and colors inside the parenthesis.
* `axes[].set_title()` - sets the bar chart's name inside the parenthesis.
* `axes[].set_ylabel()` - names the Y-axis of the bar chart inside the parenthesis.
* `plt.ylim()` - sets the Y-axis' limit specified inside the parenthesis
* `plt.tight_layout()` - organizes the overall layout as to prevent overlaps and uneven spacing between the graphs
* `fig.text()` - inserts text into the figure with the positioning, actual text, and other features such as text style being specified inside the parenthesis

```python
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

Track = df.groupby('Track')[['Average']].mean().reset_index()
Track

Gender = df.groupby('Gender')[['Average']].mean().reset_index()
Gender

Hometown = df.groupby('Hometown')[['Average']].mean().reset_index()
Hometown

import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(15, 5))

axes[0].bar(Track['Track'], Track['Average'])
axes[0].set_title('Mean Average by Track')
axes[0].set_ylabel('Mean Average')

axes[1].bar(Gender['Gender'], Gender['Average'], color='purple')
axes[1].set_title('Mean Average by Gender')

axes[2].bar(Hometown['Hometown'], Hometown['Average'], color='green')
axes[2].set_title('Mean Average by Hometown')

plt.ylim(0, 70)
plt.tight_layout()
fig.text(0,-0.1,'Interpretation\nTrack - The Communication track had the highest average score of 67.975.\nGender - Male students had the highest average score of 67.183. \nHometown - Students from Luzon recorded the highest average score of 68.083',
         style='normal')
plt.show()
```

**Thank you for reading!**

#### READMe file Version History 
September 16, 2026 - Initial READMe output created. 

September 17, 2026 - READMe output and actual code updated.



