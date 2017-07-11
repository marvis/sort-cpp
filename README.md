
### Introduction

This is a C++ implementation of SORT, a simple online and realtime tracking algorithm for 2D multiple object tracking in video sequences.
Original Python code and publication infomation found at https://github.com/abewley/sort , By Alex Bewley

This code has been tested on Windows with Visual Studio Community 2013 + OpenCV 2.4.8. It depends on OpenCV without any other libs, so theoretically it can be compiled on Linux with OpenCV support.

Detection data in The ./data folder come from the original directory of SORT. They are the *Faster* RCNN detections for the MOT benchmark sequences in the benchmark format, created by Alex Bewley.

The Hungarian algorithm implementation comes from https://github.com/mcximing/hungarian-algorithm-cpp, which is derived from [Markus Buehren's code](http://www.mathworks.com/matlabcentral/fileexchange/6543-functions-for-the-rectangular-assignment-problem).

The license is also kept to the GPLv3 License.

### Results

The overall results of code are close to those of original SORT implmentation.

Using the [MOT challenge devkit](https://motchallenge.net/devkit/) this code produces the following results.

 Sequence       | Rcll  Prcn   FAR| GT  MT  PT  ML|   FP    FN  IDs   FM|  MOTA  MOTP MOTAL
--------------- |:---------------:|:-------------:|:-------------------:|:------------------:
 TUD-Campus     | 67.4  91.0  0.34|  8   5   3   0|   24   117    8   12|  58.5  74.8  60.5
 ETH-Sunnyday   | 77.8  81.7  0.92| 30  12  15   3|  324   412   22   57|  59.2  74.6  60.3
 ETH-Pedcross2  | 51.5  89.8  0.44|133  16  61  56|  366  3037   83  118|  44.3  74.6  45.6
 ADL-Rundle-8   | 44.3  75.3  1.50| 28   6  15   7|  984  3779  109  214|  28.2  70.9  29.8
 Venice-2       | 42.6  64.7  2.77| 26   8  11   7| 1661  4098   63  112|  18.5  72.8  19.3
 KITTI-17       | 67.9  92.6  0.26|  9   1   8   0|   37   219   13   16|  60.6  72.6  62.4
 **Overall**    | 49.5  77.1  1.28|234  48 113  73| 3396 11662  298  529|  33.5  73.1  34.8


the original sort

 Sequence       | Rcll  Prcn   FAR| GT  MT  PT  ML|   FP    FN  IDs   FM|  MOTA  MOTP MOTAL
--------------- |:---------------:|:-------------:|:-------------------:|:------------------:
 TUD-Campus     | 68.5  94.3  0.21|  8   6   2   0|   15   113    6    9|  62.7  73.7  64.1
 ETH-Sunnyday   | 77.5  81.9  0.90| 30  11  16   3|  319   418   22   54|  59.1  74.4  60.3
 ETH-Pedcross2  | 51.9  90.8  0.39|133  17  60  56|  330  3014   77  103|  45.4  74.8  46.6
 ADL-Rundle-8   | 44.3  75.8  1.47| 28   6  16   6|  959  3781  103  211|  28.6  71.1  30.1
 Venice-2       | 42.5  64.8  2.75| 26   7   9  10| 1650  4109   57  106|  18.6  73.4  19.3
 KITTI-17       | 67.1  92.3  0.26|  9   1   8   0|   38   225    9   16|  60.2  72.3  61.3
 **Overall**    | 49.5  77.5  1.24|234  48 111  75| 3311 11660  274  499|  34.0  73.3  35.1

A bit worse than original SORT but not significantly. This may due to my keeping the default parameters of Kalman filters.
The speed of this implementation is at about 1800 FPS, or ~3 seconds over 5500 frames on my machine, with the Debug configuration. 


### Eval results
 
*SenseTime POI on MOT16 train*

 Sequence       | IDF1  IDP  IDR| Rcll  Prcn   FAR|   GT  MT   PT   ML|    FP    FN   IDs    FM|  MOTA  MOTP MOTAL 
--------------- |:------------- |:---------------:|:-----------------:|:----------------------:|:------------------:
 MOT16-02       | 33.5 70.5 21.9| 48.4  95.0  0.76|   54   8   33   13|   453  9200    93   176|  45.3  80.1  45.9 
 MOT16-04       | 42.4 85.7 28.1| 69.3  93.0  2.37|   83  38   25   20|  2489 14589    53   185|  64.0  83.7  64.1
 MOT16-05       | 57.9 77.8 46.1| 60.6  91.1  0.49|  125  25   72   28|   406  2683    46   106|  54.0  78.9  54.7 
 MOT16-09       | 44.1 73.0 31.6| 69.4  95.5  0.33|   25  12   12    1|   172  1611    29    50|  65.5  84.1  66.1 
 MOT16-10       | 48.8 65.3 39.0| 73.1  89.1  1.68|   54  22   30    2|  1097  3314   133   276|  63.1  77.6  64.2
 MOT16-11       | 61.3 74.0 52.4| 73.0  94.0  0.47|   69  20   38   11|   426  2473    32    76|  68.1  85.3  68.4
 MOT16-13       | 46.0 67.3 35.0| 74.9  85.5  1.93|  107  51   44   12|  1450  2874   200   300|  60.5  77.2  62.2
 **Overall**    | 29.2 51.0 20.5| 66.7  91.9  1.22|  517 176  254   87|  6493 36744   586  1169|  60.3  81.7  60.8

*deep_sort on MOT16 train*

 Sequence       | IDF1  IDP  IDR| Rcll  Prcn   FAR|   GT  MT   PT   ML|    FP    FN   IDs    FM|  MOTA  MOTP MOTAL 
--------------- |:------------- |:---------------:|:-----------------:|:----------------------:|:------------------:
 MOT16-02       | 33.5 70.5 21.9| 48.4  95.0  0.76|   54   8   33   13|   453  9201    93   177|  45.3  80.1  45.9 
 MOT16-04       | 42.4 85.7 28.1| 69.3  93.0  2.37|   83  38   25   20|  2489 14590    53   185|  64.0  83.7  64.1 
 MOT16-05       | 58.3 78.4 46.4| 60.6  91.1  0.48|  125  25   72   28|   403  2683    47   106|  54.0  78.9  54.7 
 MOT16-09       | 44.1 73.0 31.6| 69.4  95.5  0.33|   25  12   12    1|   172  1611    29    50|  65.5  84.1  66.1 
 MOT16-10       | 48.8 65.4 39.0| 73.1  89.2  1.67|   54  22   31    1|  1095  3312   129   283|  63.2  77.5  64.2 
 MOT16-11       | 61.3 74.0 52.4| 73.0  94.0  0.47|   69  20   38   11|   424  2473    32    76|  68.1  85.3  68.4 
 MOT16-13       | 46.3 67.6 35.2| 74.9  85.5  1.94|  107  52   42   13|  1455  2876   199   303|  60.4  77.1  62.1 
 **Overall**    | 29.2 51.0 20.5| 66.7  91.9  1.22|  517 177  253   87|  6491 36746   582  1180|  60.3  81.6  60.8 
