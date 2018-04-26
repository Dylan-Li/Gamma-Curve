# Gamma-Curve
#introduce gamma curve

import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import math

gamma_curve = pd.read_csv(open(r'/Users/mac/Desktop/gamma_curve.csv'))
#print(gamma_curve)

x = np.arange(0,256)
y = (gamma_curve['lux'].loc[x]-gamma_curve['lux'].loc[0])/(gamma_curve['lux'].loc[255]-gamma_curve['lux'].loc[0])
fig = plt.figure(figsize=(18,12))
plt.plot(x,(x/256)**2,'--',label='gamma2.0',color='red')
plt.plot(x,(x/256)**2.2,'--',label='gamma2.2',color='green')
plt.plot(x,(x/256)**2.4,'--',label='gamma2.4',color='blue')
plt.plot(x,y)
plt.show()
fig = plt.figure(figsize=(18,12))

#计算各阶对应的Gamma值
def list_y2(x,y2):
    for i in x:
        if i == 0:
            y2 = [0,]
        else:    
            log1 = (gamma_curve['lux'].loc[i]-gamma_curve['lux'].loc[0])/(gamma_curve['lux'].loc[255]-gamma_curve['lux'].loc[0])
            log2 = (i/255)
            i+=1
            log_v1 = math.log10(log1)
            log_v2 = math.log10(log2)
            if log_v2 != 0:
                log_v = math.log10(log1)/math.log10(log2)
                y2.append(log_v)
            elif log_v2 == 0:
                y2.append(0)
    return y2

#W-Gamma灰阶过渡不均判定
def Wgray(y2):
    for i in y2:
        print(y2[i])
        i+=1
Wgray(y2)
y_v2 = list_y2(x,y2)
plt.plot(x,y_v2)
plt.show()
