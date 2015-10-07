命令行脚本
====================

很多Python包都有命令行工具. 借助setuptools/PyPI你可以非常方便地添加有用的命令行工具到你发布包当中, 或者你想单纯发布使用Python编写
的命令行工具.

举个例子, 我们添加一个 ``funniest-joke` 的可执行命令.

在 ``setuptools.setup()`` 中有两种方法 ``scripts`` 参数或是 ``console_scripts`` 入口.

``scripts`` 参数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

第一种方法是把你的命令写在一个单独的文件中::

    funniest/
        funniest/
            __init__.py
            ...
        setup.py
        bin/
            funniest-joke
        ...

``bin/funniest-joke`` 如下::

    #!/usr/bin/env python

    import funniest
    print funniest.joke()

在``setup()`` 添加::

    setup(
        ...
        scripts=['bin/funniest-joke'],
        ...
    )

当我们安装这个包的时候, setuptools会把你的脚本复制到PATH路径下::

    $ funniest-joke

使用这种方法的好处是可以使用非Python的语言的编写, ``funniset-joke`` 可以是一个shell脚本或者其他的都可以.


``console_scripts`` 入口
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

第二种方法是通过'entry point'. setuptools 允许模块注册'entry points', 这样可以使用其他包的功能. ``console_scripts`` 也是一个'entry points'.

``console_scripts`` 允许Python的 *functions* (不是文件) 直接被注册成一个命令行工具.

下面, 我们将添加一个新文件提供命令行工具::

    funniest/
        funniest/
            __init__.py
            command_line.py
            ...
        setup.py
        ...

``command_line.py`` 仅仅只提供命令行工具(这样组织代码更方便)::

    import funniest

    def main():
        print funniest.joke()

你可以测试一下, 就像这样::

    $ python
    >>> import funniest.command_line
    >>> funniest.command_line.main()
    ...

在setup.py 中 注册 ``main()`` ::

    setup(
        ...
        entry_points = {
            'console_scripts': ['funniest-joke=funniest.command_line:main'],
        }
        ...
    )

我们安装了这个包之后, 我们就可以直接使用 ``funniest-joke`` 命令. 因为setuptools 会自动生成一个脚本, 包括导入模块, 然后在调用注册的函数.
