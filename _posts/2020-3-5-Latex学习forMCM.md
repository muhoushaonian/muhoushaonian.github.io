---
layout: post
title: LaTex学习——MCM
description: LaTex for MCM
tag: 排版
---

### 使用已完成的美赛模板


如何引用模板:

你可以选择使用Latex中已发行的模板mcmthesis[3],我是将github上面的项目clone到本地进行魔改。

项目地址:https://github.com/muyuuuu/A-customized-MCM-LaTeX-template-based-on-ctexart/tree/master


引用模板时遇到的问题及解决办法:[Before Competition]
    illegal unit of measure(pt inserted)
    Solution: \\后面的[]被LaTex误认为可选的距离参数，将其修改为\\\relax

    font shape 'OMX/cmex/m/n' in size<10.5397>
    Solution: Add \usepackage{lmodern}% http://ctan.org/pkg/lm

    编译引擎出错[latex or pdflatex]
    Solution: %!TEX program=xelatex

    Missing $ inserted
    Solution: 该句中的下划线前加'\'

### 参考

1.VSCODE + LATEX完全解决方案: https://zhuanlan.zhihu.com/p/106167792?utm_source=wechat_session&utm_medium=social&utm_oi=859150129263951872

2.一份很短的LaTex入门文档: https://liam.page/2014/09/08/latex-introduction/

3.如何使用美赛模板mcmthesis: https://liam.page/2016/01/27/how-to-use-mcmthesis/
