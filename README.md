# mirrors-china
Mirrors and registries in China to speedup your package installation.

由于许多包的存放服务器在国外，国内安装比较慢，因此本文总结了常见的包（例如Python包，Linux不同发行版的包）在国内的开源镜像，加速你的下载，提高安装体验。下面总结了PyPi，Anacoda，NPM， Docker，RubyGems，Gradle和Linux的国内镜像。

## How to use
```bash
git clone https://github.com/vra/mirrors-china
cd mirror-china
# update files in configs dir
# copy config files to destination or run shell scripts to make them take effect 
``` 

## PyPi 加速
临时加速可以用下面的命令：
```bash
pip install -i https://path/to/pypi/mirror package
```
永久使用的话，如果pip版本升级到10.0以后，可以用下面到命令来一键永久修改：
```bash
# 参考https://mirrors.tuna.tsinghua.edu.cn/help/pypi/
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```
也可以修改配置文件`pip.conf`：

- Linux/MacOS配置文件：优先级从高到低
  - 系统级：`/etc/pip.conf`
  - 用户级：`~/.config/pip/pip.conf`或`~/.pip/pip.conf`，前者优先级比后者高
  - 虚拟环境级：虚拟环境根目录下`pip.conf`

- Windows: 修改`c:/Users/xxx/pip/pip.ini`

```bash
# official doc: https://pip.pypa.io/en/stable/user_guide/
# file path: 
#   Linux/MacOS: /etc/pip.conf, or ~/.config/pip.conf, or pip/pip.conf
#   Windows: c:/Users/xxx/pip/pip.ini

# douban, may be the fastest
[global]
index-url = https://pypi.doubanio.com/simple


# ustc, doc: https://lug.ustc.edu.cn/wiki/mirrors/help/pypi
#[global]
#    index-url = https://mirrors.ustc.edu.cn/pypi/web/simple
#    trusted-host=mirrors.ustc.edu.cn


# thu, doc: https://mirrors.tuna.tsinghua.edu.cn/help/pypi/
#[global]
#    index-url = https://pypi.tuna.tsinghua.edu.cn/simple
#    trusted-host=pypi.tuna.tsinghua.edu.cn


# aliyun, doc: http://www.atjiang.com/aliyun-pip-mirror/
#[global]    
#    index-url=http://mirrors.aliyun.com/pypi/simple
#    trusted-host=mirrors.aliyun.com


# 163, no doc.
#[global]
#    index-url=https://mirrors.163.com/pypi/simple
#    trusted-host=mirrors.163.com

# tencent, doc: https://mirrors.cloud.tencent.com/help/pypi.html
#[global]
#    index-url=https://mirrors.cloud.tencent.com/pypi/simple
#    trusted-host=mirrors.cloud.tencent.com
```

本文中默认用的中科大的源，实际使用的时候，选择自己访问最快的**一个**镜像就可以了，将别的镜像设置注释掉或者删掉。


## Anaconda 包加速
Anaconda是一个Python的包管理系统，包含科学计算常用的包。通过在命令行执行下面的文件就可以使用中科大或者清华的Anaconda镜像了，注意只执行自己访问最快的镜像对应的命令。
```bash
# run this script in terminal
# ustc, doc: https://mirrors.ustc.edu.cn/help/anaconda.html
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes

# thu, doc: https://mirror.tuna.tsinghua.edu.cn/help/anaconda/
#conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
#conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
#conda config --set show_channel_urls yes
```

或者，可以通过自行编辑配置文件`.condarc`来进行设定：

- Linux/MacOS: `~/.condarc`

- Windows: `c:/Users/xxx/.condarc`

```bash
# thu, doc: https://mirror.tuna.tsinghua.edu.cn/help/anaconda/
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

## NPM 包加速
NPM 是NodeJs的包管理系统，NodeJs的包通过该命令来安装。临时使用镜像来安装某个包可以用下面的命令：
```bash
$ npm --registry http://path/to/npm/mirror install package
```
永久使用某个镜像需要修改`~/.npmrc`，加入下面的某一个镜像即可：
```bash
# file path: ~/.npmrc
# ustc, doc: https://lug.ustc.edu.cn/wiki/mirrors/help/npm
registry=http://npmreg.mirrors.ustc.edu.cn/

# taobao, doc: https://npm.taobao.org/
#registry=http://registry.npm.taobao.org/
```

## Docker 镜像加速
修改`/etc/docker/daemon.json`，加入下面的内容：
```js
// ustc, doc: https://lug.ustc.edu.cn/wiki/mirrors/help/docker
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}

// docker-cn, doc: https://www.docker-cn.com/registry-mirror 
//{
//  "registry-mirrors": ["https://registry.docker-cn.com"]
//}
```

## RubyGems 加速
```bash
# run this script in terminal
# ustc, doc: https://mirrors.ustc.edu.cn/help/rubygems.html
gem sources  #列出默认源
gem sources --remove https://rubygems.org/  #移除默认源
gem sources -a https://mirrors.ustc.edu.cn/rubygems/  #添加科大源

# thu, doc: https://mirror.tuna.tsinghua.edu.cn/help/rubygems/
#gem sources --add https://mirrors.tuna.tsinghua.edu.cn/rubygems/ --remove #https://rubygems.org/
#gem sources -l
```

## Gradle 包加速
Android Studio基于gradle构建，可使用aliyun的maven仓库进行加速。为所有Android Studio项目做配置，先定位`$GRADLE_USER_HOME`所在目录：

- Windows：默认位于`C:\Users\<user_name>\.gradle`
- Linux：默认位于`$HOME\.gradle`
- 特别声明了`$GRADLE_USER_HOME`环境变量，或在`Android Studio安装目录/bin/idea.properties`中声明了`gradle.user.home`变量：声明所在目录

在`$GRADLE_USER_HOME`（或idea.properties中的`gradle.user.home`）目录下，新建init.gradle文件（或从本仓库config/init.gradle拷贝），内容如下：

```groovy
// aliyun maven: https://maven.aliyun.com/mvn/view
allprojects {
    buildscript {
        repositories {
            maven { url 'https://maven.aliyun.com/repository/google' }
            maven { url 'https://maven.aliyun.com/repository/jcenter' }
        }
    }
    repositories {
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
    }
}
```
重启AS以生效；或将上述配置临时修改与当前AS项目的build.gradle文件中以生效。

## Git 仓库加速
[码云](http://gitee.com)提供了导入git仓库功能。对于最常用的github上的仓库，可在[码云极速下载](https://gitee.com/mirrors)查看已有镜像，或注册账号后自行新建repo从github导入，以加速访问。

## Linux 包加速
由于Linux发行版众多，配置各不相同，因此请参考下面的源下面的文档进行对应发行版的配置：
 1. 中科大: <http://mirrors.ustc.edu.cn/help>
 2. 清华：<https://mirrors.tuna.tsinghua.edu.cn/help/AOSP>
 3. aliyun: <https://opsx.alibaba.com/mirror>
 4. 163: <https://mirrors.163.com>
