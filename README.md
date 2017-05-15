# Novartis Data Challenge
The above .ipynb file contains my approach to the data challenge. I've included much of my thoughts during the analysis, but will summarize the answers here.

Questions:
1.	How can the start and end of each balance test be identified?

It was given in the prompt that the the devices were shaken vigorously at the start, and the end, of each test. Thus, I decided that the quickest way to identify these points was peak detection of the total accelerometer magnitude (Ax**2 + Ay**2 + Az**2). I then plotted the raw total acceleration magnitude signal along with a weighted moving average filtered version of signal using numpy's convolve function (Cell 65). In addition, I passed several filter windows, but a [hamming window](https://en.wikipedia.org/wiki/Window_function#Hamming_window) seemed to work the best. 

Looking at the signal alone, it was difficult to do a completely unsupervised identification of the starts and stops with just the peaks. This was particularly true as the signal seemed like it was 3 concatenated signals, with some unclear transitions between each. Thus, after performing some peak deteciton on the peaks, I manually isolated the indices of each subject (Cell 67). Plots of starts and stops for each subject are contained in Cells 68-70.  

2.	What metrics can be used as a balance score for each test?


3.	How can the balance data be visualised? 

The balance data can be visualized in many ways. I chose to plot the visualization by looking at pitch, roll, and total acceleration magnitude. Although slightly out of order, I visualized pitch and roll in Cell 71. However, as indicated in the prompt, the sensors were occasionally oriented such that the typical 'up' direction, the y-axis, was perpendicular to gravity. Looking at the roll, it's likely that the sensors were perpendicular to gravity during this period. I also scaled the x-axis to reflect time and not device cycles.

If I had more time, I would have plotted the data like [this](http://kyrandale.com/viz/d3-smartphone-walking.html). 

4.	Integrating the metadata, can you rank the difficulty of the balance tests? Can you rank the performance of the subjects?
5.	How would you advise the team on their next steps?


