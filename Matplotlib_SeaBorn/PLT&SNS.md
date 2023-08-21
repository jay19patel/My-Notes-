# Matplotlib  

- use dictionary as a data 
- Convert Dict into PD dataframe 

```py
data = {'x_values': [1, 2, 3, 4, 5],
        'y_values': [10, 15, 7, 12, 9]}
df = pd.DataFrame(data)
```



### Markers for Points 
```py
markers = ['o', 's', 'D', '^', 'v']

- "o" for round marker
- "s" for square marker
- "D" for Dimond marker
- "^" for Trengle marker up
- "v" for Trengle marker down
```
### linestyle
```py
Solid Line = '-'
Dashed Line = '--'
Dotted Line = ':'
Dash-dot Line = '-.'
```


## Plot our data in matplotlib or our plot 
### Basic Method
- if we need one graph in one frame 
```py
plt.plot(df['name'], df['age'], marker='o')  # 'o' adds markers to data points
```
### Multiple Graph
- if we need multiple graph in one frame the we use subplot
- a subplot refers to a grid of individual plots within a single figure

```py
fig, ax = plt.subplots()
ax.plot(x, x, label='Solid Line', linestyle='-')
ax.plot(x, x ** 2, label='Dashed Line', linestyle='--')
.... More....
```

### Multiple Figer in one Graph
```py
fig=plt.figure()
ax1=fig.add_subplot(111)
ax1.plot([1,2,3])
ax2=fig.add_subplot(221, facecolor='y')
ax2.plot([1,2,3])
```

## Data On axis 
```py
plt.xticks(data)
plt.yticks(data)
```
- Need to Create Tickes in our axix 
```py
plt.xlabel("X Axix Values ")
plt.ylabel("Y Axix Values ")
```
- we use xlabel for adding text into axixs (axis nu name apva mate)



# Table Name:
```py
plt.title('My First Graph etc ')
plt.grid(True)
#  if we Need Grid Box on figer 
```
# Basic Code 
import matplotlib.pyplot as plt

names = ['Alice', 'Bob', 'Charlie', 'David', 'Eva']
ages = [25, 30, 22, 28, 35]

plt.plot(names, ages, color='blue')

plt.title('Ages of Individuals')
plt.xlabel('Names')
plt.ylabel('Ages')
plt.show()


## All Graphs Methods

```py
plt.plot(x, y, marker='o', linestyle='-', color='b', label='Line Plot')
plt.bar(categories, values, color='c', alpha=0.7, label='Bar Plot')
plt.scatter(x, y, marker='o', color='r', label='Scatter Plot')
plt.hist(data, bins=5, color='purple', alpha=0.7, label='Histogram')
plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=['gold', 'yellowgreen', 'lightcoral', 'lightskyblue'])
plt.boxplot(data, vert=False)

```