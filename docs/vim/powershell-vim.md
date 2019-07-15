# 在PowerShell中使用Vim

## 1.准备好可以独立运行的vim文件
## 2.以管理员身份启动PowerShell
执行`Set-ExecutionPolicy RemoteSigned`命令,并选择Y
执行`new-item -path $profile -itemtype file -force`创建配置文件
## 3.编辑配置文件
```
set-alias vim "C:/vim/Vim81/vim.exe"
 
# To edit the Powershell Profile
# (Not that I'll remember this)
Function Edit-Profile
{
    vim $profile
}
 
# To edit Vim settings
Function Edit-Vimrc
{
    vim $HOME\_vimrc
}
```
## 4.重启PowerShell