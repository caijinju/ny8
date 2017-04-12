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

