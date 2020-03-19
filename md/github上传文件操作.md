### 使用ssh上传文件
---
##### 检查是否有ssh keys
![Image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh1.png)
---
![Image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh3.png)
##### 没有ssh keys就执行以下步骤
1. 生成 ssh keys
* 在桌面打开git命令窗口
![Image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh4.png)
```
输入 ssh-keygen -t rsa -C "邮箱" 回车确认
出现（y/n)选择y
连续3次回车，默认设置空密码 创建key
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh6.png)
2. 在本地文件夹查看 
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh5.png)
3. 查看生成的公钥
```
cat ~/.ssh/id_rsa.pub
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh7.png)
4. 复制公钥到github里添加一个SSH Key
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh8.png)
5. 测试是否添加成功
```
ssh git@github.com
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh9.png)
##### 上传本地文件
1. 在本地新建一个空文件夹 knowledgeBase
2. 再把这个文件夹变成Git可管理的仓库
```
git init
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh10.png)
> 这时你会发现knowledgeBase文件夹里面多了个.git文件夹，它是Git用来跟踪和管理版本库的，因为它默认是隐藏文件，要是看不到就设置下文件夹和搜索选项。
3. 把需要上传到github的文件复制到knowledgeBase这个目录下
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh11.png)
4. 通过git add .(注意这个"."，是有空格的，"."代表这个knowledgeBase这个文件夹下的目录全部都提交。你也可以通过git add 文件名 提交指定的文件)把文件添加到缓存区
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh12.png)
*或具体提交
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh13.png)
5. 然后可以通过git status命令，查看下现在的状态
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh14.png)
* 看到images文件夹的内容都提交上去了
6. 对本次提交的注释 双引号里面的内容可以根据个人的需要改。
```
git commit -m "注释"
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh15.png)
7. 关联远程仓库
```
git remote add origin +仓库ssh地址
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh16.png)
* ssh 查看
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh17.png)
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh18.png)
8. 关联好之后可以把本地库的所有内容推送到远程仓库（也就是github）上，通过：
```
git push -u origin master
```
* 如果新建远程仓库不是空的，例如你勾选了 Initialize this repository with a README。那么你通过命令 $ git push -u origin master是会报错的，如下：
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh19.png)
* 这是由于你新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过以下命令先将内容合并以下：
```
git pull --rebase origin master
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh20.png)
* 再输入
```
git push origin master
```
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh21.png)
### 再次上传
---
> 使用git push -u origin master 出现如下提示：

![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh22.png)
1. 警告解决方法：
```
问题分析
警告大概意思是：警告：IP地址为192.30.253.112的主机(PSA连接的)持久添加到hosts文件中
这只是一个警告不影响github的使用 可以用下列方法去除
```
C:\Windows\System32\drivers\etc
###### 本人使用的是win10 64位系统，不同系统hosts文件位置可能不同
给hosts文件添加github的IP地址
![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/ssh23.png)