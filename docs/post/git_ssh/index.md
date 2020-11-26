
老板昨天扔了个阿里云code的项目，电脑之前已经绑定了Github的账号，于是查了一下如何在同一台电脑上绑定两个账号，存档记录一下。
<!--more-->
## 1. 生成SSH key
SSH key 可以让你在你的电脑和Code服务器之间建立安全的加密连接，由于这里需要连接Github和阿里云code，所以需要生成两个ssh key，重复执行以下指令即可。
```bash
ssh-keygen -t rsa -C "your email"//github or codealiyun
```
执行以上命令后会出现以下提示，直接回车就默认在`/Users/a777/.ssh/`路径下生成`id_rsa`。

![image.png](https://i.loli.net/2020/03/14/BfpXnjJm3TKyUQe.png)

由于这里需要生成两个SSH key，所以最好修改一下文件名，由于我之前绑定github的时候直接用的默认文件名`id_rsa`，所以把阿里云code的文件名修改为`id_rsa_codealiyun`。

最后`/Users/a777/.ssh/`内的文件如下：

![image.png](https://i.loli.net/2020/03/14/uYGbdN8AjwzfQ6R.png)

## 2. 生成config
可以看到以上文件里除了密钥还有一个`config`文件，由于本地调用密钥的时默认使用`id_rsa`，所以需要一个配置文件来指定Github/阿里云code应该使用哪个ssh key。
```bash
cd /Users/a777/.ssh
vim config
```
在`config`里输入以下内容：
```bash
Host github.com 
 HostName github.com
 User hishark #这里可以输入任意名称
 IdentityFile ~/.ssh/id_rsa

Host code.aliyun.com
 HostName code.aliyun.com
 User hishark #这里可以输入任意名称
 IdentityFile ~/.ssh/id_rsa_codealiyun
```

## 3. 创建ssh key
最后在Github/阿里云Code上创建ssh key即可。
### 3.1 Github
[点击此处创建Github SSH key](https://github.com/settings/ssh/new)

<img src="https://i.loli.net/2020/03/14/mxThreuSQc2g3oP.png" width="600"/>

在key输入框中填入`id_rsa.pub`内`ssh-rsa`开头的所有字符即可。

### 3.2 阿里云Code
[点击此处创建阿里云code SSH key](https://code.aliyun.com/profile/keys/new)

<img src="https://i.loli.net/2020/03/14/8nHkR6jWZrG9T1I.png" />

在公钥输入框中填入`id_rsa_codealiyun.pub`内`ssh-rsa`开头的所有字符即可。

## 4. Done

ok现在就可以愉快了拉代码了~
