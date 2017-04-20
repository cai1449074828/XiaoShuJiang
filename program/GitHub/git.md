# git gui 
## 创建本地代码仓库
1.请在本地建立一个文件夹，名称为training,进入文件夹，初始化git版本库，同时设定你的用户名，邮件信息。

![enter description here][1]
```
git config --global user.name "cai1449074828"
git config --global user.email 1449074828@qq.com
```
## 修改提交
2.在training文件夹中，建立一个First.java源代码文件，编写输出”Hello Git”的java程序，然后添加文件，提交版本库。在提交的注释中，说明这是第一个提交的java程序，比如”first commit, java program”.

![enter description here][2]

![enter description here][3]

![enter description here][4]

![enter description here][5]

![enter description here][6]


## 版本回退
6.通过版本回退的方式，将版本退回到Second.txt文件中记录：this is a second file and also a readme file的版本。
之前都是在master分支下做的修改
需要在那个地方创建分支

![enter description here][7]
创建train分支后，使用的是train分支
修改commit后
使用之前的master分支

![enter description here][8]

![enter description here][9]
回退成功

## push远程代码仓库
生成ssh密匙

![enter description here][11]

![enter description here][10]

7.在oschina的服务器上，建立一个rjgcTrain的项目。

![enter description here][12]

8.在本地，将上题的项目的远程仓库添加到本地的remote。


![enter description here][13]

![enter description here][14]

![enter description here][15]

![enter description here][16]

9.推送本地的仓库到oschina中。

![enter description here][17]

![enter description here][18]

![enter description here][19]

![enter description here][20]


  [1]: ./images/1492051298149.jpg "1492051298149"
  [2]: ./images/1492051302419.jpg "1492051302419"
  [3]: ./images/1492051308256.jpg "1492051308256"
  [4]: ./images/1492051313095.jpg "1492051313095"
  [5]: ./images/1492051318164.jpg "1492051318164"
  [6]: ./images/1492051322936.jpg "1492051322936"
  [7]: ./images/1492051470932.jpg "1492051470932"
  [8]: ./images/1492051476510.jpg "1492051476510"
  [9]: ./images/1492051481754.jpg "1492051481754"
  [10]: ./images/1492051918512.jpg "1492051918512"
  [11]: ./images/1492051765895.jpg "1492051765895"
  [12]: ./images/1492051496057.jpg "1492051496057"
  [13]: ./images/1492051501636.jpg "1492051501636"
  [14]: ./images/1492051507032.jpg "1492051507032"
  [15]: ./images/1492051511006.jpg "1492051511006"
  [16]: ./images/1492051517631.jpg "1492051517631"
  [17]: ./images/1492051527664.jpg "1492051527664"
  [18]: ./images/1492051534783.jpg "1492051534783"
  [19]: ./images/1492051539541.jpg "1492051539541"
  [20]: ./images/1492051550419.jpg "1492051550419"