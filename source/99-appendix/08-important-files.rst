附录 H. 重要文件
==================================================

.. rubric:: 启动文件

这些文件包含系统启动后所有作为用户 Shell 的 Bash 及所有 Bash 脚本的都可用的别名和环境变量。

.. glossary::
   
   :file:`/etc/profile`
     系统全局默认值，多数是设置好环境的 (所有类 Bourne Shell，不只是 Bash [#]_)

   :file:`/etc/bashrc`
     Bash 的系统全局函数和别名。

   :file:`$HOME/.bash_profile`
     特定于用户的环境默认设置，能在每个用户的主目录里找到 (:file:`/etc/profile` 的本地版)。

   :file:`$HOME/.bashrc`
     特定于用户的 Bash 载入文件，能在每个用户的主目录里找到 (:file:`/etc/bashrc` 的本地版)。只有交互 Shell 和用户脚本读取该文件。示例 :file:`~/.bashrc` 文件见附录 M。
