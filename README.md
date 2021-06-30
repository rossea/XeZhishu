# 项目说明：
## 背景
* latex中文直书目前主要使用uplatex和xelatex。uplatex基于日文直排的传统，相对比较成熟，主要问题是大部分模板都是基于jlreq规范，与传统中文的排版有一定差别。另外uplatex的字体配置确实比较复杂。相关割注包对跨行割注都需要手工调整，比较痛苦。多年来一直感觉比较遗憾。
* xelatex在CJK环境下有很多应用。且字体配置相对方便。
* 现在的情况是，2021年6月20日，ctex更新后，在texlive2021下，对中文的字体支持已经很好了。
## 思路
本项目主要目的是测试一下xetex编译器和ctex、gezhu、ruby宏包的兼容性。尽量使用ctex宏包提供的设置功能，尽量少用XeCJK的底层设置，以求减少代码的复杂性。
测试实现中文直书的头注、割注、底注、尾注、行间注，特别是Dian YIN (yindian@ustc) 的gezhu宏包2007.09.29（下载自 https://www.newsmth.net/nForum/#!article/TeX/260509 ），可以自动跨页断行，对于割注较多的文本节省了大量调整时间。


# 目前存在的主要问题：
1. 头注不能跨页排版，需要手工调整。
2. 尾注的分割线无法删除。
3. 包含全角、半角符号的割注换行后，字间距无法控制。
4. ~~\setCJKmainfont[FallBack=SimSun-ExtB]{SimSun}在ctex中 [AutoFallback = true]属性不可用。~~
\xeCJKsetup{AutoFallBack=true} %启用AutoFallBack（本选项默认是false）

# 编译环境
* XeTeX 3.141592653-2.6-0.999993 (TeX Live 2021)
* 使用fontawesome字体显示特殊符号
* 主要字体使用SourceHanSansSC。后备字体为SourceHanSansTC
* 需要编译两边：xelatex main && xelatex main
