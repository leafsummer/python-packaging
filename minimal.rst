最小的结构
=================

让我们来看一小段代码::

    def joke():
        return (u'How do you tell HTML from HTML5?'
                u'Try it out in Internet Explorer.'
                u'Does it work?'
                u'No?'
                u'It\'s HTML5.')

这小段代码仅仅是为了展示如何打包和分发Python代码, 没有实际的用途。


选择一个包名
~~~~~~~~~~~~~~

Python 模块或者包名应该遵守以下的规则:

* 全小写
* 不要和pypi上已有的包名重复，即使你不想公开发布你的包，因为你的包可能作为其他包的依赖包
* 使用下划线分隔单词或者什么都不用(不要使用连字符)

现在把我们的函数变成一个Python module **funniest**


开始工作
~~~~~~~~~~~~~~~~~~~~~~~~

目录结构 **funniest** 如下::

    funniest/
        funniest/
            __init__.py
        setup.py

最外层的目录是我们版本管理工具的根目录, 例如 ``funniest.git`` . 子目录也叫 ``funniest`` , 代表Python module.

为了更好理解, 我们把函数 ``joke()`` 放到 ``__init__.py`` 中::

    def joke():
        return (u'How do you tell HTML from HTML5?'
                u'Try it out in Internet Explorer.'
                u'Does it work?'
                u'No?'
                u'It\'s HTML5.')

最主要的setup配置文件是 ``setup.py`` , 应该包含一行代码调用 ``setuptools.setup()`` ,就像下面这样::

    from setuptools import setup

    setup(name='funniest',
          version='0.1',
          description='The funniest joke in the world',
          url='http://github.com/storborg/funniest',
          author='Flying Circus',
          author_email='flyingcircus@example.com',
          license='MIT',
          packages=['funniest'],
          zip_safe=False)

现在我们可以在本地安装这个python包::

    $ python setup.py install

我们也可以使用开发模式安装这个包, 每次修改代码之后不用重新安装, 立即可用最新的代码.::

    $ python setup.py develop

不管用哪种方式，安装之后就可以在python中使用这个包::

    >>> import funniest
    >>> print funniest.joke()


在PyPI上发布
~~~~~~~~~~~~~~~~~~

脚本 ``setup.py`` 也是在PyPI注册和上传源码包的入口.

第一步注册这个包(包括注册包名,上传元数据,创建pypi.python.org的页面)::

    $ python setup.py register

如果从未在PyPI上发布过东西, 你需要创建一个账号, 命令行向导会一步一步告诉你怎么做.

注册之后你可以在PyPI看到这个包的页面 **funniest** :

http://pypi.python.org/pypi/funniest/0.1

尽管用户可以根据URL链接找到你的git仓库, 但是为了使用方便我们需要上传一个源码包. 用户不需要clone你的git仓库，而且可以使用安装工具
自动化安装和搜索依赖关系.

第二步创建一个源码包::

    $ python setup.py sdist

这一步会在你的顶层目录下创建 ``dist/funniest-0.1.tar.gz`` . 如果你有时间, 可以把这个文件拷贝到另一台主机上, 解压然后安装,
测试一下安装包.

第三步上传到PyPI::

    $ python setup.py sdist upload

你可以把这几步结合起来, 更新元数据, 发布新版本, 一步就完成::

    $ python setup.py register sdist upload

想要查看setup.py更多的功能可以看看帮助::

    $ python setup.py --help-commands


安装这个包
~~~~~~~~~~~~~~~~~~~~~~

上面的步骤完成之后, 其他用户可以直接用 ``easy_install`` 安装::

    easy_install funniest

或者使用 ``pip`` ::

    $ pip install funniest

如果这包作为其他包的依赖包, 它将被自动安装(我们在后面会提到如何配置)


添加其他文件
~~~~~~~~~~~~~~~~~~~~~~~

大部分时间我们的代码分散在多个文件当中,

举个例子, 我们把函数移动到一个新的文件中 ``text`` , 现在我们的目录结构是这样子的::

    funniest/
        funniest/
            __init__.py
            text.py
        setup.py

``__init__.py`` ::

    from .text import joke

``text.py`` ::

    def joke():
        return (u'How do you tell HTML from HTML5?'
                u'Try it out in Internet Explorer.'
                u'Does it work?'
                u'No?'
                u'It\'s HTML5.')

所有的代码应该都在 ``funniest/funniest/`` 目录下.


忽略的文件 (.gitignore, etc)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

我们可能需要一个 ``.gitignore`` 或者是其他代码管理工具类似的文件, 因为创建包的过程中会产生一下中间文件, 我们并不想提交到代码仓库当中.

下面是一个 ``.gitignore`` 的例子::

    # Compiled python modules.
    *.pyc

    # Setuptools distribution folder.
    /dist/

    # Python egg metadata, regenerated from source files by setuptools.
    /*.egg-info


大功告成
~~~~~~~~~~~~~~~~~~~

上面讲的结构已经包含了创建一个包的所有步骤. 如果所有的Python工具和库都遵循同样的规则来打包, 世界会更加美好.

**客官别急** 下面还有更多内容, 因为大部分的包还需要命令行脚本, 文档, 测试，分析工具等等, 请看下一篇.
