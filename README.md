# 项目说明：（无法正常使用-不再测试-不再更新）
## 背景
* latex中文直书目前主要使用uplatex和xelatex。uplatex基于日文直排的传统，相对比较成熟，主要问题是大部分模板都是基于jlreq规范，与传统中文的排版有一定差别。另外uplatex的字体配置确实比较复杂。相关割注包对跨行割注都需要手工调整，比较痛苦。多年来一直感觉比较遗憾。
* xelatex在CJK环境下有很多应用。且字体配置相对方便。
* 现在的情况是，2021年6月20日，ctex更新后，在texlive2021下，对中文的字体支持已经很好了。
## 思路
本项目主要目的是测试一下xetex编译器和ctex、gezhu、ruby宏包的兼容性。尽量使用ctex宏包提供的设置功能，尽量少用XeCJK的底层设置，以求减少代码的复杂性。
测试实现中文直书的头注、割注、底注、尾注、行间注，特别是Dian YIN (yindian@ustc) 的gezhu宏包2007.09.29（下载自 https://www.newsmth.net/nForum/#!article/TeX/260509 ），可以自动跨页断行，对于割注较多的文本节省了大量调整时间。


## 目前存在的主要问题：
1. 头注不能跨页排版，需要手工调整。
2. 尾注的分割线无法删除。
3. ~~包含全角、半角符号的割注换行后，字间距无法控制。~~ 
  目前不进行标点压缩，则不会出现割注字距的问题。
4. 割注换页后，因字号不同，页边距与其他页面不同，导致版心偏移。一个重要原因是gezhu宏包对于跨页的割注，要拆开盒子后重新封盒，新封的盒子的行间距是割注字体的行间距，与正文的行间距不同。而且修改\newcommand*\CJKmovesymbol[1]{\raise.32em\hbox{#1}} 会使文中数字和英文与所在行文字不对其。同时还会影响跨页割注和页边距的位置。
5. ~~\setCJKmainfont[FallBack=SimSun-ExtB]{SimSun}在ctex中 [AutoFallback = true]属性不可用。~~
  \xeCJKsetup{AutoFallBack=true} %启用AutoFallBack（本选项在xeCJK中默认是false）

6. ~~编译时报错，异常终止 TeX capacity exceeded, sorry [main memory size=5000000]~~ 

通过修改/usr/local/texlive/2021/texmf.cnf

在自定义字体目录

OSFONTDIR = /usr/share/fonts//;/usr/local/share/fonts//;~/.fonts//

添加以下参数，将默认数值加大

  main_memory=500000000
  
  extra_mem_bot=500000000
  
  font_mem_size=500000000
  
  pool_size=500000000
  
  buf_size=500000000


## 编译环境
* XeTeX 3.141592653-2.6-0.999993 (TeX Live 2021) in Ubuntu20.04(5.4.72-microsoft-standard-WSL2)
* 使用fontawesome字体显示特殊符号
* 主要字体使用SourceHanSansSC。后备字体为SourceHanSansTC
* 需要编译两遍：xelatex main && xelatex main

## 阶段性结论
根据目前ctex、gezhu在xelatex下对中文直书的支持程度和兼容性，实现中文直书的排版仍需要大量的工作。这些工作抵消了xelatex中文字体配置的便利。

目前成熟度比较高的方案还是uplatex下基于jlreq、等日文书籍的宏包。其中，jlreq基本可以直接使用。
