# BioimageVision-SpeedTIFF
### Fast reading of TIF images in batches, currently supported:
* 8Bit + 2D
* 8Bit + 3D
* 16Bit + 2D
* 16Bit + 3D
* Other data types have not yet been tested   

### Fast writing of TIF images in batches, currently supported:
* 8Bit + 2D
* 8Bit + 3D
* 16Bit + 2D
* 16Bit + 3D
* Other data types have not yet been tested

  
## Technique Help
quxuzhong@hust.edu.cn
## Test data
https://zenodo.org/record/8385040

## Note
**When writing pictures in batches, ensure that disk C has a large space. You are advised to write more than twice the size of each batch of pictures**
 
## Environment
```
Python==3.8
```
## Install
```
cd SpeedTifIOWhl
pip install SpeedTifIO-1.0-py3-none-any.whl
```
## Example Read
```
import os
from SpeedTifIO import SpeedReadTifClass

if __name__ == '__main__':    
    path = r'H:\TDIA1302b002_DataSet11'
    ls = os.listdir(path)
    obj = SpeedReadTifClass()
    for name in ls:
        obj.AddPath(os.path.join(path, name))
    for name in ls:
        img = obj.GetImg()
        print(name, img.shape, img.max(), img.min())
```
## Example Write
### The data in the Quick Write example is randomly generated, and the generation speed is slow, please wait
```
import os, time
from os.path import join
from SpeedTifIO.SpeedWriteTif import SpeedWriteClass
import numpy as np

if __name__ == '__main__':
    # Saved file path. Need to modify
    savePath = r'E:\SpeedWriteTifTestData'
    '''random images'''
    # random images number
    imgNumber = 20
    os.makedirs(savePath, exist_ok=True)
    imgLs = []
    for i in range(imgNumber):
        imgLs.append(np.random.randint(255, size=(32000, 40000), dtype=np.uint8))
    '''Start Speed Write'''
    print('StartWrite')
    writeObj = SpeedWriteClass()
    s1 = time.time()
    for ii in range(imgNumber):
        writeObj.AddPath(join(savePath, str(ii).zfill(5) + '.tif'), imgLs[ii])
    for ii in range(imgNumber):
        add = writeObj.WriteOk()
        name = os.path.basename(add)
        print(name, 'Finish!')
    print('TotalTime: ', time.time() - s1)
    writeObj.Close()
```
## Video Read
[The video for fast reading images](https://github.com/QuantingweiImage/BioimageVision-SpeedTIFIO/assets/41601635/c5f85bf8-ab4e-4c8c-a2a1-713db3d16004)
## Video Write
[The video for fast Writing images](https://github.com/Quanlab-Bioimage/BioimageVision-SpeedTIFF/assets/41601635/34a59c19-3ddc-47e2-bc6a-25acfa97d2c3)
