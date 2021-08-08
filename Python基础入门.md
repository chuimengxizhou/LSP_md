# Python基础入门





## 9 类

### 9.1 创建和使用类

**示例：**

```python
class Restaurant:
    def __init__(self, name, typee):
        self.name = name
        self.typee = typee

    def showname(self):
        print('name is', self.name)

    def showtype(self):
        print("type is", self.typee)

    def intro(self):
        s = "a " + self.typee + "'s restautant called " + self.name
        return s


mine = Restaurant("susan", 'USA')
print("name is", mine.name)
print(mine.intro())

```





### 9.2 修改属性的值

1.直接访问

```python
class Car:
    def __init__(self, name, speed, trait):
        self.name = name
        self.speed = speed
        self.trait = trait

    def intro(self):
        s = self.name + "'s " + self.speed + " is quick"
        return s


mine = Car('sbbf', '220', 'nb')
mine.name = '666np'
print(mine.intro())

```

2.间接修改(依靠内置方法)

```python
class Car:
    def __init__(self, name, speed, trait):
        self.name = name
        self.speed = speed
        self.trait = trait

    def intro(self):
        s = self.name + "'s " + self.speed + " is quick"
        return s
    def update_name(self,newname):
        self.name=newname

mine = Car('sbbf', '220', 'nb')
mine.update_name('python')
print(mine.intro())

```





### 9.3 继承

#### 9.3.1 子类的方法

```python
class Car:
    def __init__(self, name, speed, trait):
        self.name = name
        self.speed = speed
        self.trait = trait

    def intro(self):
        s = self.name + "'s " + self.speed + " is quick"
        return s

    def update_name(self, newname):
        self.name = newname

    def show(self):
        print(self.trait)


class AIcar(Car):
    def __init__(self, name, speed, trait):
        super()._init_(name, speed, trait)  # 初始化父类的属性
        self.battery = 75  # 定义新的属性和方法

    def show(self):  # 重写并覆盖父类方法
        print(self.speed)

```





















## **10 文件和异常**



### 10.1 读取整个文件

**函数：**open（）

**作用：**接受一个参数——要打开文件的路径

**示例：**

```python
with open('xxx.txt') as fp:#全部打印
    contents = fp.read()
print(contents.rstrip())

```

```python
with open('xxx.txt') as fp:#逐行打印
    for line in fp:
        print(c.rstrip())

```

```python
with open('xxx.txt') as fp:#包含文件各行的列表
    lines = fp.readlines()
for l in lines:
    print(l.rstrip())
    
```





### 10.2 文件路径

（1）相对路径：从当前路径开始的路径。

（2）绝对路径：从盘符开始的路径。





### 10.3 写入文件

**示例：**

```python
filename = 'xxx.txt'
sstr = "alabama"
with open(filename, 'w') as fp:
    fp.write(sstr)#只能写入字符串

```

**注意：**

（1）若写入文件不存在，将创建该文件；若存在，会清空该文件再写。

（2）读取（‘r’）；写入（'w'）；附加（'a'）；读写（'r+'）





### 10.4 异常处理

#### 1. ZeroDivisionError异常

**处理代码块：**try - except - else

**示例：**

```python
a, b = input().split()
try:#将可能引发错误的代码放在这里
    ans = eval(a) / eval(b)
except ZeroDivisionError:
    print("ZDE error")
else:
    print(ans)
    
```





#### 2. FileNotFoundError异常

**示例：**

```python
try:
    with open('sfvrsb.txt','r') as fp:
        cts = fp.read()
except FileNotFoundError:
    print("File not exist")
else:
    print(cts)

```





### 10.5 静默失败

```python
try:
    with open('sfvrsb.txt', 'r') as fp:
        cts = fp.read()
except FileNotFoundError:
    pass#不会有提示
else:
    print(cts)

```





### 10.6 储存数据

**模块：**json

**函数：**json.dump()

​			json.load()

**示例：**

```python
import json as js

filename = 'username.json'
try:
    with open('username.json', 'r') as fp:
        cts = js.load(fp)#读存数据
except FileNotFoundError:
    n = input("your name:")
    with open("username.json", 'w') as f:
        js.dump(n, f)#转存数据
        print("hello!", n)
else:
    print("welcome", cts)

```











## 12 Pygame



import pygame

##### **初始化pygame库**

pygame.init()


##### 窗口相关操作
创建窗口

window = pygame.display.set_mode([窗口宽, 窗口高])

设置窗口标题

pygame.display.set_caption("窗口标题")

加载资源图片，返回图片对象

image = pygame.image.load("res/game.ico")

设置窗口图标

pygame.display.set_icon(image)

指定坐标，将图片绘制到窗口

window.blit(image, (0, 0))


##### 图像相关操作
加载图片文件，返回图片对象

image = pygame.image.load("图片路径")

获得图片矩形对象 -> Rect(x, y, width, height)

默认情况下左上角的坐标是 (0, 0)

rect = image.get_rect(centerx=x, centery=y)

在原位置基础上，移动指定的偏移量 (x, y 增加)

rect.move_ip(num1, num2)

判断两个矩形是否相交，相交返回True，否则返回False

flag = pygame.Rect.colliderect(rect1, rect2)

将图片对象按指定宽高缩放，返回新的图片对象

trans_image = pygame.transform.scale(image, (WINDOWWIDTH, WINDOWHEIGHT))


##### 事件相关操作
常见事件类型：

QUIT　关闭窗口

KEYDOWN　键盘按键

获得当前所有持续按键 bools_tuple

获得所有事件的列表

event_list = pygame.event.get()

for event in event_list:
    1. 鼠标点击关闭窗口事件
        if event.type == pygame.QUIT:
        print("关闭了窗口")
        sys.exit()
        2. 键盘按下事件
            if event.type == pygame.KEYDOWN:
             判断用户按下的键是否是a键
            if event.key == pygame.K_a:
                print("按了 a ")
            if event.key == pygame.K_UP:
                print("按了 方向键上")

3. 获得当前键盘所有按键的状态(按下，没有按下)，返回bool元组

pressed_keys = pygame.key.get_pressed()

if pressed_keys[pygame.K_w] or pressed_keys[pygame.K_UP]:
    print("按了 w 键，或者 方向键上")


##### 音效相关操作
加载背景音乐

pygame.mixer.music.load("./res/音乐文件名")

循环播放背景音乐

pygame.mixer.music.play(-1)

停止背景音乐

pygame.mixer.music.stop()

加载音效

boom_sound = pygame.mixer.Sound("./res/音效名")

播放音效

boom_sound.play()

停止音效

boom_sound.stop()

三基色：Red Green Blue


0 ~ 255

##### 文字显示操作

font = pygame.font.SysFont('SimHei', 字体大小)

render(text(文本内容), antialias(抗锯齿), color(RGB))，返回文字对象

textobj = font.render(text, 1, (200, 200, 200))

设置文字矩形对象位置

textrect = textobj.get_rect()
textrect.move_ip(水平偏移量, 竖直偏移量)

在指定位置绘制指定文字对象

window.blit(textobj, textrect)

更新界面

pygame.display.update()








