命令行脚本
====================

很多Python包都有命令行工具. 借助setuptools/PyPI你可以非常方便地附加一下有用的命令行工具到你发布的当中, 或者单纯发布使用Python编写
的命令行工具.
Many Python packages include command line tools. This is useful for distributing support tools which are associated with a library, or just taking advantage of the setuptools / PyPI infrastructure to distribute a command line tool that happens to use Python.

举个例子, 我们添加一个``funniest-joke`的可执行命令.
For **funniest**, we'll add a ``funniest-joke`` command line tool.

在``setuptools.setup()``中有两种方法``scripts``参数或是``console_scripts``入口.
There are two mechanisms that ``setuptools.setup()`` provides to do this: the ``scripts`` keyword argument, and the ``console_scripts`` entry point.

``scripts`` 参数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

第一种方法是把你的命令写在一个单独的文件中::
The first approach is to write your script in a separate file, such as you might write a shell script.::

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
When we install the package, setuptools will copy the script to our PATH and make it available for general use.::

    $ funniest-joke

使用这种方法的好处是可以使用非Python的语言的编写, ``funniset-joke``可以是一个shell脚本或者其他的都可以.
This has advantage of being generalizeable to non-python scripts, as well: ``funniset-joke`` could be a shell script, or something completely different.


``console_scripts`` 入口
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

第二种方法是通过'entry point'. setuptools 允许模块注册'entry points', 这样可以使用其他包的功能. ``console_scripts``也是一个'entry points'.
The second approach is called an 'entry point'. Setuptools allows modules to register entrypoints which other packages can hook into to provide certain functionality. It also provides a few itself, including the ``console_scripts`` entry point.

``console_scripts`` 允许Python的*functions* (不是文件) 直接被注册成一个命令行工具.
This allows Python *functions* (not scripts!) to be directly registered as command-line accessible tools.

这样,我们将添加一个新文件提供命令行工具::
In this case, we'll add a new file and function to support the command line tool::

    funniest/
        funniest/
            __init__.py
            command_line.py
            ...
        setup.py
        ...

``command_line.py`` 仅仅只提供命令行工具(这样组织代码更方便)::
The ``command_line.py`` submodule exists only to service the command line tool (which is a convenient organization method)::

    import funniest

    def main():
        print funniest.joke()

你可以测试一下, 就像这样::
You can test the "script" by running it directly, e.g.::

    $ python
    >>> import funniest.command_line
    >>> funniest.command_line.main()
    ...

在setup.py 中 注册``main()``::
The ``main()`` function can then be registered like so::

    setup(
        ...
        entry_points = {
            'console_scripts': ['funniest-joke=funniest.command_line:main'],
        }
        ...
    )

我们安装了这个包之后, 我们就可以直接使用``funniest-joke`` 命令. 因为setuptools 会自动生成一个脚本, 包括导入模块, 然后在调用注册的函数.
Again, once the package has been installed, we can use it in the same way. Setuptools will generate a standalone script 'shim' which imports your module and calls the registered function.

