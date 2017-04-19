## 版本0.1.11 -- 统一命令高亮

## 添加

寄存器（包括R、F、S）高亮显示，高亮形式为 SpecialKey

---

## 版本0.1.10 -- 统一命令高亮

## 修改

1. 所有汇编命令高亮统一为 Directory
2. 所有NYASM命令高亮统一为 PreCondit

---

## 版本0.1.9 -- 修复Label没向后缩进问题

### BUG

问题

- label在输入冒号之后没有向后缩进

修复

1. 在indentkeys添加冒号 `<:>`

```
setlocal indentkeys=break,else,endfor,endif,ends,endsw,endw,until,endc,endm,<:>
```

2. 修改label行的匹配

```
let nyasm_indent_label_line= '^\s*' . nyasm_identifier_regex . '\s*:'
```

3. 添加当前行为label向后缩进处理

```
if this_line =~? nyasm_indent_label_line
  let ind = ind - &sw
endif
```

### 修改

1. 取消label行增加缩进的返回操作，改为赋值继续执行
2. 取消macro行增加缩进的返回操作，改为赋值继续执行



---

## 版本0.1.8 -- 修复macro缩进问题

### BUG

问题

- macro缩进格式错误！单输入macro可缩进；macro前有macroName则无法缩进

修复

- 去掉macro在`nyasm_indent_begin_regex`中的定义
- 另外重新定义macro的缩进

```
let nyasm_indent_macro_line='^\s*' . nyasm_identifier_regex . '\s\+macro\>'

if previous_line =~ nyasm_indent_macro_line
  return ind + &sw
endif

```

### 修改

1. 匹配标号内容整合为标号行

```
let nyasm_indent_label_line= '^\s*' . nyasm_identifier_regex . '\s*:\s*\(' . nyasm_comment_regex . '\)\?$'

if previous_line =~ nyasm_indent_label_line
  return ind + &sw
endif

```

2. 将tabstop改为4

```
setlocal tabstop=4
```

---

## 版本0.1.7 -- 修复标号高亮问题
### BUG

问题

- 标号后有空格再添加冒号，则不高亮

修复

- 修改匹配模式，在自定义标号后添加空白，再添加标号，内容如下：

```vim
syn match nyasmLabel		/[A-Za-z_@][A-Za-z0-9_@]*\s*:/me=e-1
```

### 修改

修改添加2种新高亮颜色 -- ModeMsg 和 MoreMsg

```
hi def link othIns	ModeMsg
hi def link condInst	MoreMsg
```


