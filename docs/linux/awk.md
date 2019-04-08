

awk变量 | 含义
---|---
$0 | 当前记录（这个变量中存放着整个行的内容）
$1~$n | 当前记录的第n个字段，字段间由FS分隔
FS | 输入字段分隔符 默认是空格或Tab
NF | 当前记录中的字段个数，就是有多少列
NR | 已经读出的记录数，就是行号，从1开始，如果有多个文件话，这个值也是不断累加中
FNR | 当前记录数，与NR不同的是，这个值会是各个文件自己的行号
RS | 输入的记录分隔符， 默认为换行符
OFS | 输出字段分隔符， 默认也是空格
ORS | 输出的记录分隔符，默认为换行符
FILENAME | 当前输入文件的名字

```
> 	netstat > netstat.txt
$ awk '{print $1, $4}' netstat.txt
$ awk '{printf "%-8s %-8s %-8s %-18s %-22s %-15s\n",$1,$2,$3,$4,$5,$6}' netstat.txt
$ awk '$3==0 && $6=="LISTEN" ' netstat.txt
```

1. 指定分隔符
```
awk  'BEGIN{FS=":"} {print $1,$3,$6}' /etc/passwd
```
等价于
```
awk  -F: '{print $1,$3,$6}' /etc/passwd
```
2. 多个分隔符
```
awk -F '[;:]'
```
3.  分隔符输出
```
$ awk  -F: '{print $1,$3,$6}' OFS="\t" /etc/passwd
```
4. 字符串匹配
```
awk '$6 ~ /FIN/ || NR==1 {print NR,$4,$5,$6}' OFS="\t" netstat.txt
awk '$6 ~ /WAIT/ || NR==1 {print NR,$4,$5,$6}' OFS="\t" netstat.txt
#sed风格匹配
awk '/LISTEN/' netstat.txt
#复杂模式匹配
awk '$6 ~ /FIN|TIME/ || NR==1 {print NR,$4,$5,$6}' OFS="\t" netstat.txt
#模式取反
awk '$6 !~ /WAIT/ || NR==1 {print NR,$4,$5,$6}' OFS="\t" netstat.txt
awk '!/WAIT/' netstat.txt
```
5. 拆分文件
```
#按第六列拆分文件，NR!=1表示不处理表头
awk 'NR!=1{print > $6}' netstat.txt
#按指定列输出
awk 'NR!=1{print $4,$5 > $6}' netstat.txt
#更复杂的例子
awk 'NR!=1{if($6 ~ /TIME|ESTABLISHED/) print > "1.txt";
else if($6 ~ /LISTEN/) print > "2.txt";
else print > "3.txt" }' netstat.txt
```
6. 统计
```
#计算所有的C文件，CPP文件和H文件的文件大小总和。
ls -l  *.cpp *.c *.h | awk '{sum+=$5} END {print sum}'
#统计各个connection状态
awk 'NR!=1{a[$6]++;} END {for (i in a) print i ", " a[i];}' netstat.txt
#统计每个用户的进程占了多少内存
ps aux | awk 'NR!=1{a[$1]+=$6;} END { for(i in a) print i ", " a[i]"KB";}'
```

7. awk脚本
```
#范例文件
cat score.txt
Marry   2143 78 84 77
Jack    2321 66 78 45
Tom     2122 48 77 71
Mike    2537 87 97 95
Bob     2415 40 57 62

#awk脚本
$ cat cal.awk
#!/bin/awk -f
#运行前
BEGIN {
    math = 0
    english = 0
    computer = 0
 
    printf "NAME    NO.   MATH  ENGLISH  COMPUTER   TOTAL\n"
    printf "---------------------------------------------\n"
}
#运行中
{
    math+=$3
    english+=$4
    computer+=$5
    printf "%-6s %-6s %4d %8d %8d %8d\n", $1, $2, $3,$4,$5, $3+$4+$5
}
#运行后
END {
    printf "---------------------------------------------\n"
    printf "  TOTAL:%10d %8d %8d \n", math, english, computer
    printf "AVERAGE:%10.2f %8.2f %8.2f\n", math/NR, english/NR, computer/NR
}
```

执行：
```
awk -f cal.awk score.txt
#或
./cal.awk score.txt
```
8. 环境变量 通过-v参数
```
 awk -v val=$x '{print $1, $2, $3, $4+val, $5+ENVIRON["y"]}' OFS="\t" score.txt
```

9. 几个例子
```
#从file文件中找出长度大于80的行
awk 'length>80' file
 
#按连接数查看客户端IP
netstat -ntu | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr
 
#打印99乘法表
seq 9 | sed 'H;g' | awk -v RS='' '{for(i=1;i<=NF;i++)printf("%dx%d=%d%s", i, NR, i*NR, i==NR?"\n":"\t")}'
```