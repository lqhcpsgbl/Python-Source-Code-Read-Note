# hello world

##《Python源码剖析》 笔记，基于Python 2.7.16

Include 包含了C语言的头文件
Lib 包含了自带的Python语言标准库
Modules 包含了对性能要求高的C语言标准库模块
Parser 包含了扫描器和解释器代码
Objects 包含了Python内置对象的代码
Python 包含了编译器和执行引擎部分代码

修改Python源码并运行：

修改内置对象Objects中的 `intobject.c` 文件：

```c
/* ARGSUSED */
static int
int_print(PyIntObject *v, FILE *fp, int flags)
     /* flags -- not used but required by interface */
{
    long int_val = v->ob_ival;
    Py_BEGIN_ALLOW_THREADS
    fprintf(fp, "show an integer from console:");  // 新增代码行
    fprintf(fp, "%ld", int_val);
    Py_END_ALLOW_THREADS
    return 0;
}
```

重新make并进入解释器：

```python
➜  Python-2.7.16 make && ./python.exe 
>>> print 1
show an integer from console:1
```

说明修改成功了。

关于 Py_ssize_t ，其实就是一个整型
typedef ssize_t Py_ssize_t;


