# OpenCV

## opencv-python

### 学习测试实例

*PythonApplication1.py*

```Python
Python 3.10
numpy 1.23.0
opencv-python 4.5.5
```

```Python
import cv2
import numpy
import copy
```

#### 读取图像

```Python
img = cv2.imread("beauty.png")
```

#### 创建窗口

```Python
W1 = cv2.namedWindow("W1") 
```

#### 显示图像

```Python
def cv_show(windowname, img):
    cv2.imshow(windowname, img)
    key =  cv2.waitKey()
    if key & 0xFF == ord('q'):
        cv2.destroyAllWindows()

cv_show("picture_show", img)
```

#### 保存图像

```Python
r = cv2.imwrite("beauty-out.png", img)
if r==True:
    print("图像保存成功！")
    print(type(img))

cv2.waitKey(0)  # 无限等待按键
```

#### 创建黑白图

```Python
img2 = numpy.zeros((16,16), dtype=numpy.uint8) # 该函数默认全为0

cv2.imshow("img-2", img2)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 灰度图

```Python
img3 = cv2.imread("E:/beauty.png", 0) # 单通道灰度 读取图像

cv2.imshow("img-3", img3)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 通过索引改变图像

```Python
for i in range(100,601):
    for j in range(200,300):
        img[i,j] = 255

cv2.imshow("img-4", img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 生成一副彩色随机图像

```Python
img5 = numpy.random.randint(0,256,size=[500,500,3],dtype=numpy.uint8)

cv2.imshow("img-5", img5)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 图像通道拆分

```Python
b = img[:,:,0]
g = img[:,:,1]
r = img[:,:,2]

cv2.imshow("img-b", b)
cv2.imshow("img-g", g)
cv2.imshow("img-r", r)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 图像通道合并

```Python
rgb = cv2.merge([r, g ,b])

cv2.imshow("b->r, g->g, r->b", rgb)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 变量测试

```Python
imgg = img      # 这两个变量指向同一内存
imgg[:,:,0]=0
cv2.imshow("imgg",imgg)
print(id(img),id(imgg))
```

#### 使用copy模块进行 浅拷贝&深拷贝

```Python
imgg = copy.copy(img)
print(id(imgg),id(img))
print(type(imgg),type(img))
```

#### 图像加法

```Python
# +
img6 = numpy.random.randint(0,256,size=[500,500],dtype=numpy.uint8)
img7 = numpy.random.randint(0,256,size=[500,500],dtype=numpy.uint8)
img8 = img6 + img7

cv2.imshow("img6",img6)
cv2.imshow("img7",img7)
cv2.imshow("img8",img8)
cv2.waitKey(0)
cv2.destroyAllWindows()

# add()
imgg = img
img1 = cv2.add(img, imgg)
img2 = img + imgg

cv2.imshow("add()",img1)
cv2.imshow("+",img2)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 图像加权和

```Python
p1 = cv2.imread("E:/p1.png")
p2 = cv2.imread("E:/p2.png")
mixp = cv2.addWeighted(p1,0.6,p2,0.4,50)

cv2.imshow("mixp",mixp)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 图像位运算

```Python
a = numpy.zeros(img.shape,dtype=numpy.uint8)
a[100:800,300:1000] = 255
b = cv2.bitwise_and(img,a)

cv2.imshow("a & img",b)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 位平面提取

```Python
imgg = cv2.imread("E:/beauty.png",0)
r,c = imgg.shape
x = numpy.zeros((r,c),dtype=numpy.uint8)
x[:,:] = 2**7
imgg = cv2.bitwise_and(imgg,x)
mask = imgg[:,:]>0
imgg[mask] = 255

cv2.imshow("imgg",imgg)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 提取肤色区域

```Python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h,s,v = cv2.split(hsv)
minHue = 5
maxHue = 170
hueMask = cv2.inRange(h, minHue, maxHue)
minSat = 25
maxSat = 166
satMask = cv2.inRange(s, minSat, maxSat)
mask = hueMask & satMask
roi = cv2.bitwise_and(img, img, mask = mask)

cv2.imshow("ROI", roi) 
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 调整HSV

```Python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h,s,v = cv2.split(hsv)
v[:,:,] = 255
newhsv = cv2.merge([h,s,v])
art = cv2.cvtColor(newhsv, cv2.COLOR_HSV2BGR)

cv2.imshow("art", art)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### BGRA alpha通道

```Python
bgra = cv2.cvtColor(img, cv2.COLOR_BGR2BGRA)
b,g,r,a = cv2.split(bgra)
a[:,:] = 10
new_bgra = cv2.merge([b,g,r,a])

cv2.imshow("new_bgra", new_bgra)
cv2.imwrite("new_bgra.png", new_bgra)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 图像几何变换

```Python
rst = cv2.resize(img, None, fx=0.6, fy=0.6) # 放缩
dst = cv2.flip(img, 6)                      # 翻转

h,w = img.shape[:2]                         #平移
x = 100
y = 200
M = numpy.float32([[1, 0, x], [0, 1, y]])
move = cv2.warpAffine(img, M, (w, h))

M2 = cv2.getRotationMatrix2D((w/2, h/2), 45, 0.6)   # 旋转
rotate = cv2.warpAffine(img, M2, (w, h))

cv2.imshow("rst", rst)
cv2.imshow("dst", dst)
cv2.imshow("move", move)
cv2.imshow("rotate", rotate)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 阈值处理

```Python
t, rst = cv2.threshold(img, 136, 255, cv2.THRESH_BINARY)
t2, rst2 = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY_INV)
imgg=cv2.imread("E:/beauty.png", 0)
t3, rst3 = cv2.threshold(imgg, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)     # 似乎不支持彩色

print(t, "\n", rst)
print(t2, "\n", rst2)
print(t3, "\n", rst3)
cv2.imshow("rst", rst)
cv2.imshow("rst2", rst2)
cv2.imshow("rst3", rst3)

cv2.waitKey(0)
cv2.destroyAllWindows() 
```

#### Canny边缘检测

```Python
imgg = cv2.imread("E:/beauty.png", 0) # 单通道灰度 读取图像
r = cv2.Canny(imgg, 24, 80)

cv2.imshow("r", r)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

#### 图像金字塔

```Python
down = cv2.pyrDown(img)
down_up = cv2.pyrUp(down)
diff = img - down_up

cv2.imshow("diff", diff)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
