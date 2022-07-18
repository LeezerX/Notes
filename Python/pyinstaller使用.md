#! https://zhuanlan.zhihu.com/p/543003527
# pyinstaller的使用

pyinstaller是一个用于将py脚本打包成exe可执行文件的python模块.

## 模块安装
用pip安装即可,推荐使用国内镜像安装.[^1]

```powershell
python -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyinstaller
```


若出现问题,可直接在github的[pyinstaller库](https://github.com/pyinstaller/pyinstaller.git)寻找答案.

## 模块使用
正常情况下,pyinstaller会将python解释器下的所有模块给导入exe,这会导致编译的程序非常大.
为了减小程序体积,可以用pipenv来创建虚拟环境,在pipenv中安装所需要的模块和pyinstaller后,在pipenv中进行转换exe.

同样,用
```powershell
python -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pipenv
```
来安装pipenv即可.

### 使用流程
```powershell{.line-numbers}
# 在终端下输入指令
pipenv install # 创建pipenv虚拟环境

pipenv shell # 启动虚拟环境

# 创建虚拟环境后,会在目录中创建一个pipfile文件,用记事本打开后,将url替换成国内镜像源:https://pypi.tuna.tsinghua.edu.cn/simple,不然后面在pipenv中安装模块会奇慢无比.

pipenv install ... # 安装该程序所依赖的所有模块

pipenv install pipinstaller # 别忘了安装最重要的哦

# 下面进行程序打包
pipinstaller -F -w -i icon.ico main.py

### 执行完这个等待即可.
    ### 其中
        ## -F 表示打包单个py脚本
        ## -i 表示给打包的程序添加个图标,如果不要,就将-i icon.ico取掉即可.记:icon.ico是你要使用的图标的文件名,且要紧跟在-i后面
        ## -w 在windows系统下,加上-w就不会跳出黑框框了,如果有GUI或者用turtle画图可以加上这个.
```

进行完上述操作后,就可在目录中的dist文件夹中找到可执行程序

### 将mp3文件一并打包入程序

有时,会想在程序中添加音频,这里可以使用pygame模块[^2]来完成.其代码如下:


```python{.line-numbers}
from pygame import mixer # 只导入相关模块,可以减小程序体积

# 播放一首歌
mixer.init() 
track = mixer.music.load(filepath) # 加载音乐,filepath为音乐的路径
mixer.music.set_volume(0.3) # 设置音量
mixer.music.play(loops=1) # loops表示音乐播放的次数,play表示开始播放音乐

# 播放多首歌
track = mixer.Sound(filepath) # 载入音乐,filepath为音乐文件的路径
mixer.music.set_volume(1.0) # 设置音量
track.play() # 开始播放,同样有loops参数.播放不同的歌,重新载入Sound()即可
```

这里,为了将音乐文件一起打包进exe程序中,即exe外可以不附带音乐文件直接运行,我们需要这样来获取音乐文件的filepath

```python{.line-numbers}
def resource_path(relative_path):
    if getattr(sys, 'frozen', False): #是否Bundle Resource
        base_path = sys._MEIPASS
    else:
        base_path = os.path.abspath(".")
    return os.path.join(base_path, relative_path)

filepath = resource_path(os.path.join("file","xx.mp3"))
```

这里file是音乐文件所在的子文件夹(为了将mp3打包进exe,需要将音乐文件存放在和py文件同目录的子文件夹中,xx.mp3即为要播放的音乐文件).
程序的目录结构如下:

```
--root
    -- main.py # 主程序
    -- icon.ico # 图标文件
    -- res # 存放音乐文件的文件夹
        -- 1.mp3
        -- 2.mp3
        -- ...
```

然后,再执行上述的pyinstaller使用指令.会在root文件夹中,发现一个**main.spec**文件,用记事本打开,将里面的**data=[\]**,改为**data=[('file','file')]**,其中,file为你存放音乐文件的文件夹的名字.

最后再执行下面这个指令就完成了

```
pyinstaller main.spec
```

[^1]:python -m用于指定安装给哪个python解释器,如果只装了一个python,可以忽略

[^2]:音乐用MP3格式
