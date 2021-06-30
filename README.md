# Git操作手册
### clone篇
通常是通过命令git clone来down仓库，但是由于国内访问github都比较慢，因此我们这里有个“离线下载”的思路，c4games组织下engine-x我们已经在https://gitee.com/adxeproject 组织下创建了镜像（相当于我们的离线下载服务器），然后我们初次clone的时候就可以直接从gitee下载源码（国内100M宽带，clone速度都非常快），详细命令如下:  
clone仓库: ```git clone https://gitee.com/adxeproject/adxe```   
clone完成后，可通过如下方式修改为你实际fork的url地址:  
* 直接编辑.git/config文件，修改[remote "origin"]的url和pushurl后保存即可
* 通过命令修改:  
```sh
git remote set-url origin https://github.com/<your git acount>/adxe
git remote set-url --push origin https://github.com/<your git acount>/adxe
git remote add official https://github.com/adxeproject/adxe.git
```  

### PR篇
提交PR有两种方式
1. 代码改动少，可以直接通过网页操作在主仓库打开要修改的文件，点击右上侧“笔”按钮进行编辑，由于一般来讲，对主仓库没有提交权限，修改完成路一路点绿色按钮就可以创建PR了, 如果有写权限，则注意会有个单选按钮，请选择create new branch后再点击绿色按钮(Propose file change)，一路next即可创建PR
2. 代码改动较多，一般需要本地测试，而且可能有多个文件修改，此时一般通过remote命令增加1个自己fork的remote
```sh
  # we assume you already add remote `official`
  # Sync official remote
  git fetch official
  # create a branch from official latest for PR source branch
  git checkout -b feature1 official/dev
  # After finish changes on branch feature1, push it to your fork repo
  git push origin feature1
  # Then, please goto github page to create pull-request step by step.
```
**注: 在PR合并之前，PR源分支的任何修改都会同步表现在PR评论区，也就是PR合并时包含PR开始到合并的每一条提交记录**

### Review篇
通常，可以再github网页上review代码，但如果想先合并PR在本地验证review，则可通过如下命令先merge远程pr到本地来跑代码验证:  
```sh
git fetch origin pull/219/head:pr219
git checkout pr219
```
或者直接合并远程PR到本地当前分支
```
git pull origin pull/219/head
```
其中219是PR的id, pr219是本地分支名称
