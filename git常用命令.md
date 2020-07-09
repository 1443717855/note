

## 克隆项目 

 - git clone 项目地址

## 拉取项目  
- git pull 

## 上传项目 git push 

## 新建分支 
 - git branch 分支名

## 切换分支 
- git checkout 分支名

## 配置全局的name 和email 

- git config --global user.name "name" 

- git config --global user.email "email" 

## 生成SSH Key

- ssh-keygen -t rsa -C "youremail"  

- 会在你C:\Users\Administrator\.ssh的目录里有个id_rsa.pub文件 用记事本打开复制里面的值

## git merge 本地子分支

- 当你拉去了线上主分支到本地但是你并不想直接在上面更改，而是新建一个本地分支来进行更改，当你更改完成之后需要切回到主分支然后合并子分支

## git branch -D 分支名

- 删除指定分支