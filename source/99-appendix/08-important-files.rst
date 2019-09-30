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

.. rubric:: 登出文件

.. glossary::
   
   :file:`$HOME/.bash_logout`
     特定于用户的指令文件，能在每个用户的主目录里找到。只有交互 Shell 和用户脚本读取该文件。退出登录 (Bash) Shell 时，会执行该文档里的指令。

.. rubric:: 数据文件

.. glossary::
   
   :file:`/etc/passwd`
     系统上所有用户，及他们的身份、主目录、所属组、和默认 Shell 的列表。注意用户密码 *并没有* 被存储在这个文件 [#]_ ，而是加密存储在 :file:`/etc/shadow` 中。

.. rubric:: 系统配置文件

.. glossary::
   
   :file:`/etc/sysconfig/hwconf`
     已连接的硬件设备的列表和描述。该信息为文本形式，并可以提取和解析。

     .. code-block:: console

        $ grep -A 5 AUDIO /etc/sysconfig/hwconf	      
        class: AUDIO
         bus: PCI
         detached: 0
         driver: snd-intel8x0
         desc: "Intel Corporation 82801CA/CAM AC'97 Audio Controller"
         vendorId: 8086

     .. note:: 该文件存在于 Red Hat 和 Fedora Core 安装中，但可能在其他发行版中不存在。

.. rubric:: 脚注

.. [#] 这不适用于 **csh**, **tcsh**, 及其他与经典 Bourne Shell (**sh**) 无关或不衍生的 Shell。
.. [#] UNIX 早期版本中，密码 *确实* 存储在 :file:`/etc/passwd` 中，这便解释了文件的命名。
