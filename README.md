### A beginner’s approach to COVID-19 Data Visualization using matplotlib in Python

> Apocalypse takes place when we least expect it to happen.

It feels surreal to imagine how the virus began to spread from one person that is patient zero to four million today. It was possible because of the transport system. Earlier back in the days we didn’t have a fraction of the transportation system we have today.

Well, what good practices you can follow for now is to sanitize your grocery products and keep them idle for a day or two. Until we find a vaccine that could be years away from us, keeping social distance in public places is the only way to reduce the number of cases. Make sure you take vitamin C in the form of additional tablets or in the form of food. Well, it’s not going to prevent you from getting corona, but at least if you get infected, your immunity is going to be stronger than the person who didn’t take it to fight the virus. The last practice is to replace your handshakes with Namaste or Wakanda Salute.

![](https://cdn-images-1.medium.com/max/1042/1*hgKeK8rTPA4XzRKqjnF0kQ.gif)![](https://cdn-images-1.medium.com/max/781/1*s_-zQu-BjfDWH-rxoh7ozQ.gif)

### TASKS

![](https://cdn-images-1.medium.com/max/1042/1*uR1INXi4Gjh6dp6UlYEzQg.gif)

### Let’s get started…

We will be going through some basic plots available in matplotlib and make it more aesthetically pleasing.

### Here are the Visualizations we’ll be designing using matplotlib

*   Simple Plot?—?Date handling
*   Pie Chart
*   Bar Plot

<pre>import numpy as np
import pandas as pd
import matplotlib.pyplot as plt</pre>

We import matplotlib.pyplot library as plt

### Initializing Dataset

Importing Dataset on Covid-19 India case time series

<pre>data = pd.read_csv('case_time_series.csv')</pre>

![](https://cdn-images-1.medium.com/max/1042/1*neEOdh3bXmflSBY6RzwfiQ.png)

case_time_series.csv dataset has 7 column

Collecting Daily Confirmed ,Daily Recovered and Daily Deceased in variables as array.

<pre>Y = data.iloc[61:,1].values #Stores Daily Confirmed
R = data.iloc[61:,3].values #Stores Daily Recovered
D = data.iloc[61:,5].values #Stores Daily Deceased</pre>

<pre>X = data.iloc[61:,0] #Stores Date</pre>

‘_Y’_ variable stores the ‘Daily Confirmed’ corona virus cases

‘_R’_ variable stores the ‘Daily Recovered’ corona virus cases

‘D_’_ variable stores the ‘Daily Deceased’ corona virus cases

And ‘X’ variable stores the ‘Date’ column

### 1] Plotting Simple Plot?—?Date handling

We’ll be following the object oriented method for plotting.

plot( Passing x?—?axis value first and followed by Y?—?axis value )

Call matplotlib’s plot function by _plt.plot()_

The plot function takes two arguments that is X axis values and Y axis values plot( Passing x?—?axis value first and followed by Y?—?axis value )

<pre>plt.plot(X,Y)</pre>

In this case we have passed the ‘X’ variable which has ‘Dates’ and ‘Y’ variable which has ‘Daily Confirmed’ to plot.

![](https://cdn-images-1.medium.com/max/1042/1*bQDpzQ5qFjMGBAdt8bsQ9Q.png)

Simple Plot

We get a Simple Plot on execution of above code which looks like this where X?—?axis has Dates and Y?—?axis has Number of Confirmed cases. But this is not the best representation for a large dataset values along the axes as you can see the ‘Dates’ are overlapping on X?—?axis. To overcome this challenge we will introduce some new functions to take more control over the aesthetics of the graph.

### Aesthetics

To have control over the aesthetics of the graph such as labels, titles, color and size we shall apply more functions as shown below.

<pre>plt.figure(figsize=(25,8))</pre>

This creates a canvas for the graph where the first value ‘25’ is the width argument position and ‘8’ is the height argument position of the graph.

<pre>ax = plt.axes()</pre>

Lets create an object of the axes of the graph as ‘ax’ so it becomes easier to implement functions.

<pre>ax.grid(linewidth=0.4, color='#8f8f8f') </pre>

‘.grid’ function lets you create grid lines across the graph. The width of the grid lines can be adjusted by simply passing an argument ‘linewidth’ and changing its color by passing ‘color’ argument.

<pre>ax.set_facecolor("black") 
ax.set_xlabel('\nDate',size=25,color='#4bb4f2')
ax.set_ylabel('Number of Confirmed Cases\n',size=25,color='#4bb4f2')</pre>

‘.set_facecolor’ let’s you set the background color of graph which overe here is balck.

‘.set_xlabel’ and ‘.set_ylabel’ let’s you set the label along both axes whose size and color can be be altered .

<pre>ax.plot(X,Y,color='#1F77B4',marker='o',linewidth=4,markersize=15,markeredgecolor='#035E9B')</pre>

Now we plot the graph again with ‘X’ as Dates and ‘Y’ as Daily Confirmed by calling plot function. The plotting line ,marker and color can be altered by passing color, linewidth?—?to change color and adjust the width of plotting line and marker, markersize, markeredgecolor?—?to create marker which is circle in this case, adjust size of the marker and define marker’s edge color.

After executing above lines of code we get…

![](https://cdn-images-1.medium.com/max/1042/1*rw6C_mTskHMdJr4G6HcpTA.png)

Still as we can see the dates are overlapping and the labels along axes are not clear enough. So now we are going to change the ticks of the axes and also annotate the plots.

<pre>plt.xticks(rotation='vertical',size='20',color='white')
plt.yticks(size=20,color='white')
plt.tick_params(size=20,color='white')</pre>

‘.xticks’ and ‘.yticks’ let’s you alter the Dates and Daily Confirmed font.For the Dates to not overlap with each other we are going to represent them vertically by passing ‘rotation = vertical’. To make the ticks easily readable we change the font color to white and size to 20.

‘.tick_params’ let’s you alter the size and color of the dashes which look act like bridge between the ticks and graph.

<pre>for i,j in zip(X,Y):
    ax.annotate(str(j),xy=(i,j+100),color='white',size='13')</pre>

‘.annotate’ let’s you annotate on the graph. Over here i have written a code to annotate the plotted points by running a for loop which plots at the plotted points. The str(j) holds the ‘Y’ variable which is Daily Confirmed. Any string passed will be plotted. The xy is the coordinates where the string should be plotted. And finally the color and size can be defined. Note i have added +100 to j in xy coordinates so that the string doesn’t overlaps with marker and it is at the distance of 100 units on Y?—?axis.

<pre>ax.annotate('Second Lockdown 15th April', xy=(15.2, 860),xytext=(19.9,500),color='white',size='25',arrowprops=dict(color='white',linewidth=0.025))</pre>

To annotate an arrow pointing at a position in graph and its tail holding the string we can define ‘arrowprops’ argument along with its tail coordinates defined by ‘xytext’. Note that ‘arrowprops’ alteration can be done using a dictionary.

<pre>plt.title("COVID-19 IN : Daily Confrimed\n",size=50,color='#28a9ff')</pre>

Finally we define a title by ‘.title’ and passing string ,its size and color.

After running above lines of codes we get…

![](https://cdn-images-1.medium.com/max/1042/1*8eA04gqrxmWcBLcQq401rg.png)

### 2] Pie Chart

We’ll be plotting the Transmission Pie Chart to understand the how the virus is spreading based on Travel, Place Visit and Unknown reason.

### Initializing Dataset

<pre>slices = [62, 142, 195]
activities = ['Travel', 'Place Visit', 'Unknown']</pre>

So we have created a list slices based on which our Pie Chart will be divided and the corresponding activities are it’s values.

### PLOTTING PIE CHART

<pre>cols=['#4C8BE2','#00e061','#fe073a']
exp = [0.2,0.02,0.02]</pre>

<pre>plt.pie(slices,labels=activities, textprops=dict(size=25,color='black'),
radius=3,
colors=cols,
autopct='%2.2f%%',
explode=exp,
shadow=True,
startangle=90)</pre>

<pre>plt.title('Transmission\n\n\n\n',color='#4fb4f2',size=40)</pre>

To plot a Pie Chart we call ‘.pie’ function which takes x values which is ‘slices’ over here base on it the pie is divided followed by labels which has the corresponding string the values it represents. These string values can be altered by ‘textprops’. To change the radius or size of Pie we call ‘radius’. For the aesthetics we call ‘shadow’ as True and ‘startangle ’= 90\. We can define colors to assign by passing a list of corresponding colors. To space out each piece of Pie we can pass on list of corresponding values to ‘explode’. The ‘autopct’ defines the number of positions that are allowed to be shown. In this case autopct allows 2 positions before and after decimal place.

After executing above lines of code…

![](https://cdn-images-1.medium.com/max/1042/1*TZWT9gR3DooXmfzY19I6Qw.png)

### 3] Bar Plot

Now we are going to plot the most common type of graph which is bar plot. Over here w will be ploting the district wise corona virus cases for a state.

### Initializing Dataset

<pre>data = pd.read_csv('district.csv')
data.head()</pre>

![](https://cdn-images-1.medium.com/max/1042/1*NBia00n0RI46rhCxS-BMcQ.png)

<pre>re=data.iloc[:30,5].values
de=data.iloc[:30,4].values
co=data.iloc[:30,3].values
x=list(data.iloc[:30,0])</pre>

‘re’ stores Recovered corona patients count for all districts.

‘de’ stores Deceased corona patients count for all districts.

‘co’ stores Confirmed corona patients count for all districts.

‘x’ stored District names.

### Plotting Bar Chart

<pre>plt.figure(figsize=(25,10))
ax=plt.axes()</pre>

<pre>ax.set_facecolor('black')
ax.grid(linewidth=0.4, color='#8f8f8f')</pre>

<pre>plt.xticks(rotation='vertical',size='20',color='white')#ticks of X
plt.yticks(size='20',color='white')</pre>

<pre>ax.set_xlabel('\nDistrict',size=25,color='#4bb4f2')
ax.set_ylabel('No. of cases\n',size=25,color='#4bb4f2')</pre>

<pre>plt.tick_params(size=20,color='white')</pre>

<pre>ax.set_title('Maharashtra District wise breakdown\n',size=50,color='#28a9ff')</pre>

The code for aesthetics will be same as we saw in earlier plot. Only thing that will change is calling for the bar function.

<pre>plt.bar(x,co,label='re')
plt.bar(x,re,label='re',color='green')
plt.bar(x,de,label='re',color='red')</pre>

<pre>for i,j in zip(x,co):
    ax.annotate(str(int(j)),xy=(i,j+3),color='white',size='15')</pre>

<pre>plt.legend(['Confirmed','Recovered','Deceased'],fontsize=20)</pre>

To plot a bar graph we call ‘.bar’ and pass it x-axis and y-axis values. Over here we called the plot function three times for all three cases (i.e Recovered , Confirmed, Deceased) and all three values are plotted with respect to y-axis and x-axis being common for all three which is district names. As you can see we annotate only for Confirmed numbers by iterating over Confirmed cases value. Also we have mentioned ‘.legend’ to indicate legends of the graph.

![](https://cdn-images-1.medium.com/max/1042/1*VrKbpv9wZYWzh-xUKuuKtg.png)

Link to the datasets (CSV): Click [here](https://www.dropbox.com/sh/nqs6lnd050thzdi/AABl-GNnKu-u04Ee1G27li7Ba?dl=0)

Thanks for swinging by and checking out my article on _‘A beginner’s approach to COVID-19 Data Visualization using matplotlib in Pyhton’._

To see the above graphs ,seaborn and plotly in action (Pyhton code included): [https://smarthardik10.github.io/COVID-19-INDIA-DATA-VISUALIZATION/](https://smarthardik10.github.io/COVID-19-INDIA-DATA-VISUALIZATION/)

My GitHub repository : [https://github.com/smarthardik10](https://github.com/smarthardik10)

### **Thanks..**

And Stay Safe 😷
