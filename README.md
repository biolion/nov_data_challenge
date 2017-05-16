# Novartis Data Challenge
The above .ipynb file contains my approach to the data challenge. I've included much of my thoughts during the analysis, but will summarize the answers here.

Questions:
1.	How can the start and end of each balance test be identified?

It was given in the prompt that the the devices were shaken vigorously at the start, and the end, of each test. Thus, I decided that the quickest way to identify these points was peak detection of the total accelerometer magnitude (Ax**2 + Ay**2 + Az**2). I then plotted the raw total acceleration magnitude signal along with a weighted moving average filtered version of signal using numpy's convolve function (Cell 65). In addition, I passed several filter windows, but a [Blackman window](https://en.wikipedia.org/wiki/Window_function#Blackman_window) seemed to work the best. 

Looking at the signal alone, it was difficult to do a completely unsupervised identification of the starts and stops with just the peaks. This was particularly true as the signal seemed like it was 3 concatenated signals, with some unclear transitions between each. Thus, after performing some peak deteciton on the peaks, I manually isolated the indices of each subject (Cell 67). Plots of starts and stops for each subject are contained in Cells 68-70.  

2.	What metrics can be used as a balance score for each test?

I can think of two easy measures of global activity and stability. The first is looking at the total signal energy deviation from the mean. The lower the signal energy, the better. The second is looking at the coefficient of variation of the signal. In other words, how variable the signal is (std/mean).
The results were interesting in that I could see places where the total acceration magnitude was small, but the pitch angle did change quite a bit. I've visualized each test for each subject in Cells 72,106, and 107. Note that the cells are not contiguous in number, but do follow eachother. I've also calculated the results of thge signal deviation from mean and coefficient of variation tests for botht the pitch and total acceleration magnitudes. I've also included the metadata in the results, where a '0' is a pass and a '1' is a fail.


3.	How can the balance data be visualised? 

The balance data can be visualized in many ways. I chose to plot the visualization by looking at pitch, roll, and total acceleration magnitude. Although slightly out of order, I visualized pitch and roll in Cell 71. However, as indicated in the prompt, the sensors were occasionally oriented such that the typical 'up' direction, the y-axis, was perpendicular to gravity. Looking at the roll, it's likely that the sensors were perpendicular to gravity during this period. I also scaled the x-axis to reflect time and not device cycles.

Also, I've visualized each test for each subject in Cells 72,106, and 107. Note that the cells are not contiguous in number, but do follow eachother.

If I had more time, I would have plotted the data like [this](http://kyrandale.com/viz/d3-smartphone-walking.html). 

4.	Integrating the metadata, can you rank the difficulty of the balance tests? Can you rank the performance of the subjects?

There are lots of ways to rank performance. I've calculated some interesting statistics from the pitch and acceleration signals. It's hard to do this in a fair way. Because I'm nearly out of time, it might be best to just assume that a 'pass' is '0' and a 'fail' is a '1'. Then use the rank function and do a bunch of rank and sums to skew the difficulty of a test to favor the metadata results (i.e., make sure the failed tests are ranked low). The lower the ranking the easier.

My final ranking can be seen in the final colum of the last cell of the notebook (Cell 113).

5.	How would you advise the team on their next steps?

My next steps would largely center around evaluation and visualization the data. From the prompt, little is known about what indications we're looking for. We don't know what constitutes a 'fail' or 'pass' on the balance tests. If we knew more about what information the researchers are intested in obtaining, we may better be able to align the data collection and analysis aspects with their research goals. For instance, if we are interested in balance data, it may help to automatically generate data concerning whether or not the subject is within a calibrated angle. In doing so, we might be able to better 'grade' the subjects performance (e.g., <2 times per test outside of the calibrated range is a pass. [2,6) is an average, and >6 is a fail).

In addition, if
