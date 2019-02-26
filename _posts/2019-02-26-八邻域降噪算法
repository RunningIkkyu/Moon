---
layout: post
title:  "八邻域降噪算法"
date:   2019-02-26
excerpt: "一种简单的八邻域降噪算法, 通过扫描像素周围区域, 根据给定阈值判断是否去除该点"
tag:
- python
- CV
comments: true
---

## 算法思想:
对于图像(二值化后的灰度图像)任意一个像素点(x,y), 扫描其周围八个方向的像素点, 如果其邻域出现的背景色个数大于某一特定值(比如4), 则认为该点为噪声点, 将其去除.

## 优缺点
该算法适合处理单像素的点噪和线噪, 效果很好, 但是对于粗线条的噪声去除效果不好.

## 代码
利用python和PIL模块对该算法进行实现:
```python
from PIL import Image

def denoise(img, threshold):
    """这里已经假设传进来的图像是经过灰度转换和二值化处理的"""
    def get_white_around(img, x, y):
        """计算某像素点周围背景像素点(白色)的数量
        count = 0
        width, height = img.size
        for i in [x-1, x, x+1]:
            for j in [y-1, y, y+1]:
                if i == x and j == y:
                    continue
                if x-1 < 0 or x+1 > width-1:
                    count = count + 1
                    continue
                if y-1 < 0 or y+1 > height-1:
                    count = count + 1
                    continue
                if img.getpixel((i,j)) == 255:
                    count = count + 1
        return count

    width, height = img.size
    for i in range(width):
        for j in range(height):
            if img.getpixel((i,j)) == 255:
                # 如果像素点是背景色就不需要处理了
                continue
            if get_white_around(img, i, j) > threshold:
                img.putpixel((i,j), 255)
    return img


if __name__ == "__main__":
    print("opening pic")
    img = Image.open("a.png")
    print("denosing")
    newimg = denoise(img, 4)
    print("saving")
    newimg.save("b.png")

```


处理前的图片:
![submission image](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/a.png)

经过八邻域降噪后的图片:
![submission image](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/b.png)

可以看到, 对于小的噪点和细的线条去除效果立竿见影,但是对于粗线条的去除效果不是很想理想, 甚至没什么效果.
