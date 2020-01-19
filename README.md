## FMCW radar signal filtering  

The goal was to simulate moving target, and detect it with FMCW (continuous-wave) radar using range-dopler map.  

#### Problem statement  

In real conditions, the radar recieves signals not only from objects of interest, but also from the environment and other unwanted objects. These signals often called "clutter noise". So we need to apply some robust filtering algorithm to estimate noise level and pick objects with "strong" signal. Let's use **constant false alarm rate (or CFAR)** for doing that.  

#### 2D CFAR algorithm step by step  

1. Determine the number of Training (TR, TD) and Guard (GR, GD) cells for range and doppler dimensions. Guard cells needed to avoid the target signal from leaking into the training cells, that could adversely affect the noise estimate. Number of training cells should be not so large, since we could supress "target" signals.  
2. Slide the Cell Under Test (CUT) across the complete range-doppler map.  
3. Convert the collected values to linear scale and measure the average of the noise across all the training cells. This gives the threshold. 
4. Add the offset (multiply in case of linear scale) to the threshold to keep the false alarm to the minimum.  
8. Determine the signal level at the Cell Under Test (the one that not in the train/guard cells).  
9. If the CUT signal level is greater than the Threshold, assign a value at the CUT index to 1, else equate it to zero.  
10. Since the cell under test are not located at the edges, due to the training cells occupying the edges, we suppress the edges to zero by initiating the thresholded array with zeros, and only fill indeces which passed the test.   

