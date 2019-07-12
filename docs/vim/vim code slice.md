## 代码片段
知识点：

+ 声明变量
+ 字符串连接
+ @/寄存器（搜索默认寄存器）
+ 利用字符串分段声明实现正则表达式注解
+ 正则非捕获组

```vim
" demo.vim
" (level, msg) = drcMsg(gKwDRCName, 41, \"pad (%s), default func_sel (%s) in Function(%s) must have signal"%(CodName, func_value, func_value), Loc_Info(gKwCoDesignView, idx+2, 'Funcion'+str(func_value)))

let $pat = ""
let $pat .= "^\\(\\s*\\)(level, msg)\\s*=\\s*"          " -> (level, msg) =
let $pat .= "drcMsg("                                   " -> drcMsg( 
let $pat .= "\\(\\w\\+\\)\\s*,"                         " -> gKwDRCName,
let $pat .= '\s*\(\d\+\)\s*,'                           " -> 41,
let $pat .= '\s*\("[^"]\+"\s*\%(%([^()]\+)\)\?\)\s*,'   " -> \"pad (%s), default func_sel (%s) in Function(%s) must have signal\"%(CodName, func_value, func_value), 
let $pat .= "\\s*\\(.*\\))\s*"                          " -> Loc_Info(gKwCoDesignView, idx+2, 'Funcion'+str(func_value)))
let $pat .= "\\n\\s*objLog.log(level, msg)\s*"
let $pat .= "\\n\\s*if level == logging.CRITICAL or (objArgs.ignore is False and level == logging.ERROR):\\s*"
let $pat .= "\\n\\s*raise Exception\\s*"
echo $pat
let @/ = $pat
"/\s*(level, msg)\s*=\s*drcMsg(\(\w\+\)\s*,\s*\(\d\)\s*,\s*\("[^"]\+"\s*\(%([^()]\+)\)\?\)\s*,\s*\(.*\))\s*\n\s*objLog.log(level, msg)\s*\n\s*&sss
"/
"%s//\1'''&'''\r\1drc_item = \2\r\1drc_num  = \3\r\1drc_msg  = \4\r\1drc_loc  = \5\r\1drc_check(drc_item, drc_num, drc_msg, drc_loc)/g
%s//\1drc_item = \2\r\1drc_num  = \3\r\1drc_msg  = \4\r\1drc_loc  = \5\r\1drc_check(drc_item, drc_num, drc_msg, drc_loc)/g
noh

```