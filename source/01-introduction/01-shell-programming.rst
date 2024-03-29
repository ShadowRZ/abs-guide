1. 是 Shell 编程！
==================================================

   No programming language is perfect. There is not even a single best language; there are only languages well suited or perhaps poorly suited for particular purposes.
   
   --Herbert Mayer

一个良好的 Shell 脚本知识是任何想要在系统管理方面变得相当娴熟的人们的必备知识，即使他们不期待实际去写一个脚本。
考虑到当 Linux 机器启动的时候，会执行 :file:`/etc/rc.d` 里的 Shell 脚本来还原系统配置，配置好服务。对这些启动脚本的详细了解，就对分析系统行为，及更改它们的可能非常重要。

掌握脚本编写的技术并不难，因为脚本可以一块一块地构造，且要学习的 Shell 特定操作符 [#]_ 和参数相对较小。语法也简单——简朴到就像在命令行调用与连接工具那样简单，而且只有一小部分「规则」管理其使用。大多数较短的脚本初用就能工作，调试更长的脚本也比较直观。

   | 在早期的个人计算机时代，BASIC 给予任何熟悉电脑的人在早期一代电脑上编写程序的能力。
   | 几个世纪后，Bash 脚本语言给予任何对 Linux 或 UNIX 有着基本知识的人做同样的事情。
   |
   | 我们现在有了功能惊叹的小型单板计算机，比如 `树莓派 (Raspberry Pi) <https://www.raspberrypi.org>`_ 。Bash 编程给予我们一种探索这些迷人设备的方法。

Shell 语言是一个又快又“脏乱差”的复杂程序原型构造方法。让有限的一部分功能在脚本里工作通常是项目开发有用的第一步。这样的话，程序结构就可以在用 *C*, *C++*, *Java*, *Perl* 或 *Python* 最终编写前测试、调试、以及发现大问题。

Shell 脚本编写起源于经典的，将复杂项目分解成更简单的小任务，再到连接组件和工具的过程。许多人把它当成一种比用像 *Perl* 这样新一代高赋能的全能语言更好，或者说更美观的解决问题的方式。那些编程语言尝试当所有人的万能锦囊，但代价是强迫你改变你的思维模式以适应这种语言。

据 Herbert Mayer 说，“一个有用的编程语言要有数组、指针、及一种构建数据结构的通用方法。”按照这些要求，Shell 脚本某种程度上属于「有用」，或者说，可能不……

.. admonition:: 何时不用 Shell 脚本

   * 资源敏感任务，尤其是在速度方面敏感 (排序、哈希、递归 [#]_ 等)
   * 涉及到重型数学运算，尤其是浮点数、任意精度计算及复合数字 [#T1]_ (请改用 *C++* 或 *FORTRAN*)
   * 需要跨平台兼容性 (请改用 *C* 或 *Java*)
   * 必须结构化编程的复杂程序 (变量类型检查、函数原型等)
   * 赌上公司未来的关键程序
   * *安全性* 至关重要的场合，即你需要保证系统确定性，保护其免受干扰、骇客攻击、架构破坏等风险。
   * 包括带互相交替依赖组件的项目 [#T2]_
   * 需要广泛文件操作 (*Bash* 局限于线性文件访问，且仅是尤其笨拙还低效的按行处理)
   * 需要原生支持多维数组
   * 需要链表或树状结构等数据类型
   * 需要生成 / 操作图像或 GUI
   * 需要直接访问系统硬件及外界设备
   * 需要端口或 Socket I/O
   * 需要使用库或与老式代码交互
   * 专有，闭源软件 (Shell 脚本代码公开给所有人阅读)

   若符合以上条件，考虑一下更强大的脚本语言——可能是 *Perl*, *Tcl*, *Python*, *Ruby*——又或者是如 *C*, *C++*, *Java* 这样的编译型语言。
   即便如此，用 Shell 脚本开发程序原型可能还是开发中有用的一步。

我们将会使用 Bash，Bourne-Again shell 的缩写词 [#]_ (又是对 Stephen Bounce 的经典 *Bourne* shell 的笑话)。Bash
已经成为大多数 UNIX 变种的 Shell *事实* 标准。本书涵盖的大多数概念在其他 Shell 中可同等应用，如 Bash 从中衍生部分功能的 *Korn Shell* [#]_ 以及 *C Shell* 和其他变种。(注意 *C Shell* 编程由于 Tom Christiansen 于 1993 年十月 `在 Usenet 发文中 <http://www.faqs.org/faqs/unix-faq/shell/csh-whynot/>`_ 指出的其各种神错误而不被推荐)

接下来的就是 Shell 编程教程。它高度依赖示例来展示 Shell 的各种功能。这些脚本能够工作 [#T3]_ ——因为它们已经经受尽可能地测试——有些甚至在实际生活中非常有用。读者可以尝试一下源码归档中的可工作示例 (:file:`scriptname.sh` 或 `
:file:`scriptname.bash`) ，给它们加上可执行权限 (``chmod +x scriptname``)，然后运行它们看看会发生什么。如果你没有源码归档，就从其 HTML 或 PDF 渲染版中复制粘贴。注意一些展示的脚本有还未解释的功能，这可能需要读者暂时跳到后面得到启示。

除非注明，本书原作者编写了随后的脚本。

   His countenance was bold and bashed not.
   
   --Edmund Spenser

.. rubric:: 脚注

.. [#] 它们被叫做 Builtins，Shell 内部功能。
.. [#] 尽管你 *可以* 在 Shell 中用递归，但它慢死了，且语法真是乱成一团。
.. [#] *缩写词* 是一种将几个词的首字母提出来，变为顺口词的变换词。This morally corrupt and pernicious practice deserves appropriately severe punishment. Public flogging suggests itself. (译注：此段意义不明)
.. [#]  许多 *ksh98* 功能，甚至一些来自更新的 *ksh93* 的功能被加入到 Bash 中。
.. [#] 惯例上用户编写的 Bourne-shell 兼容脚本通常带有 ``.sh`` 后缀。系统脚本，如在 :file:`/etc/rc.d` 里发现的那些，不必遵从这一点。
.. [#T1] 译注：没学过 Complex Number，翻译可能不准。
.. [#T2] 译注：暂定翻译
