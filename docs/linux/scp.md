# scp 命令示例

1.  实例1：从远处复制文件到本地目录
```
$scp root@10.6.159.147:/opt/soft/demo.tar /opt/soft/
```
说明： 从10.6.159.147机器上的/opt/soft/的目录中下载demo.tar 文件到本地/opt/soft/目录中

2. 实例2：从远处复制到本地
```
$scp -r root@10.6.159.147:/opt/soft/test /opt/soft/
```
说明： 从10.6.159.147机器上的/opt/soft/中下载test目录到本地的/opt/soft/目录来。

3. 实例3：上传本地文件到远程机器指定目录
```
$scp /opt/soft/demo.tar root@10.6.159.147:/opt/soft/scptest
```
说明： 复制本地opt/soft/目录下的文件demo.tar 到远程机器10.6.159.147的opt/soft/scptest目录

4. 实例4：上传本地目录到远程机器指定目录
```
$scp -r /opt/soft/test root@10.6.159.147:/opt/soft/scptest
```
说明： 上传本地目录 /opt/soft/test到远程机器10.6.159.147上/opt/soft/scptest的目录中