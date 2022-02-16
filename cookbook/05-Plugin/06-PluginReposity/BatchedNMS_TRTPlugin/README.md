# batchedNMSPlugin
+ Use to do batched Non-Maximum Suppression operation (TensorRT built-in Plugin) [link](https://github.com/NVIDIA/TensorRT/tree/main/plugin/batchedNMSPlugin).
+ Not compatible for TensorRT8, need several edition before using in ensorRT8.
+ input tensor:
    - [0]: (nBatchSize,nBox,nClass,nBoxParameter)   float32,    Box
    - [1]: (nBatchSize,nBox,nClass)                 float32,    Score
+ input parameter:
    - [0]: shareLocation                            int32,
    - [1]: backgroundLabelId                        int32,
    - [2]: numClasses                               int32,
    - [3]: topK                                     int32,
    - [4]: keepTopK                                 int32,
    - [5]: scoreThreshold                           float32,
    - [6]: iouThreshold                             float32,
    - [7]: isNormalized                             int32,
+ output tensor:
    - [0]: (nBatchSize,1)                           int32,      number of output
    - [1]: (nRetainSize,4)                          float32,    number of non-max suppressed box
    - [2]: (nRetainSize,nKeepTopK)                  float32,    score for the box
    - [3]: (nRetainSize,nKeepTopK)                  float32,    class for the box

# Envionment：
+ nvcr.io/nvidia/tensorrt:21.06-py3 (including CUDA 11.3.1, cudnn 8.2.1, TensorRT 7.2.3.4)

# Quick start：
```shell
python3 testBatchedNMSPlugin.py
```

# Result:
```
[TensorRT] INFO: Detected 2 inputs and 4 output network tensors.
Succeeded building engine!
input data:
 [[0.    0.    0.016 0.016 0.007]
 [0.    0.    0.016 0.016 0.007]
 [0.    0.    0.016 0.016 0.01 ]
 [0.    0.    0.016 0.019 0.009]
 [0.    0.    0.016 0.027 0.007]
 [0.    0.    0.016 0.034 0.006]
 [0.    0.    0.016 0.04  0.006]
 [0.    0.    0.016 0.054 0.004]
 [0.    0.    0.016 0.07  0.004]
 [0.    0.    0.016 0.197 0.008]
 [0.016 0.    0.031 0.016 0.005]
 [0.016 0.    0.031 0.016 0.004]
 [0.016 0.    0.031 0.016 0.005]
 [0.016 0.    0.031 0.019 0.004]
 [0.016 0.    0.031 0.026 0.003]
 [0.016 0.    0.031 0.034 0.002]
 [0.016 0.    0.031 0.04  0.002]
 [0.016 0.    0.031 0.053 0.001]
 [0.016 0.    0.031 0.068 0.001]
 [0.016 0.    0.031 0.209 0.003]
 [0.031 0.    0.047 0.017 0.007]
 [0.031 0.    0.047 0.017 0.006]
 [0.031 0.    0.047 0.016 0.008]
 [0.031 0.    0.047 0.019 0.006]
 [0.031 0.    0.047 0.027 0.003]
 [0.031 0.    0.047 0.036 0.002]
 [0.031 0.    0.047 0.043 0.002]
 [0.031 0.    0.047 0.055 0.002]
 [0.031 0.    0.047 0.07  0.002]
 [0.031 0.    0.047 0.206 0.005]]
() (2000, 4) (2000,) (2000,)
outputH0:
 37
outputH1:
 [[0.344 0.096 0.359 0.166]
 [0.203 0.092 0.219 0.16 ]
 [0.188 0.092 0.203 0.16 ]
 [0.172 0.092 0.188 0.159]
 [0.359 0.097 0.375 0.166]
 [0.25  0.092 0.266 0.162]
 [0.328 0.095 0.344 0.165]
 [0.266 0.093 0.281 0.163]
 [0.234 0.092 0.25  0.161]
 [0.219 0.092 0.234 0.161]
 [0.281 0.093 0.297 0.164]
 [0.156 0.092 0.172 0.159]
 [0.312 0.095 0.328 0.164]
 [0.297 0.094 0.312 0.164]
 [0.141 0.088 0.156 0.157]
 [0.453 0.091 0.469 0.167]
 [0.438 0.091 0.453 0.168]
 [0.375 0.091 0.391 0.166]
 [0.391 0.091 0.406 0.167]
 [0.469 0.091 0.484 0.167]
 [0.406 0.091 0.422 0.166]
 [0.422 0.091 0.438 0.169]
 [0.484 0.092 0.5   0.169]
 [0.156 0.    0.172 0.018]
 [0.172 0.    0.188 0.016]
 [0.078 0.    0.094 0.019]
 [0.344 0.107 0.359 0.156]
 [0.25  0.106 0.266 0.154]
 [0.266 0.106 0.281 0.154]
 [0.094 0.    0.109 0.017]
 [0.312 0.107 0.328 0.155]
 [0.281 0.106 0.297 0.154]
 [0.297 0.107 0.312 0.154]
 [0.141 0.    0.156 0.018]
 [0.188 0.    0.203 0.016]
 [0.328 0.001 0.344 0.018]
 [0.312 0.    0.328 0.019]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]
 [0.    0.    0.    0.   ]]
outputH2:
 [1.    1.    1.    1.    1.    1.    1.    1.    1.    1.    1.    1.    0.999 0.999 0.998 0.998 0.998 0.997 0.997 0.997 0.995 0.993 0.991 0.971 0.971 0.955 0.95  0.938 0.932 0.931 0.928 0.925 0.915
 0.89  0.844 0.807 0.787 0.    0.    0.    0.    0.    0.    0.    0.    0.    0.    0.    0.    0.   ]
outputH3:
 [ 0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0.  0. -1. -1. -1. -1. -1. -1. -1. -1. -1. -1. -1. -1.
 -1.]

```