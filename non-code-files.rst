Adding Non-Code Files
=====================

通常我们的包都需要一下不是python代码的文件, 例如图片, 数据, 文档等等. 为了让setuptools正确处理这些文件, 我们需要特别定义一下这些文件.
Often packages will need to depend on files which are not ``.py`` files: e.g. images, data tables, documentation, etc. Those files need special treatment in order for setuptools to handle them correctly.

我们需要在``MANIFEST.in``中指定这些文件, ``MANIFEST.in``提供了一个文件清单, 使用相对路径或是绝对路径指出打包时需要包含的特殊文件.
The mechanism that provides this is the ``MANIFEST.in`` file. This is relatively quite simple: ``MANIFEST.in`` is really just a list of relative file paths specifying files or globs to include.::

    include README.rst
    include docs/*.txt
    include funniest/data.json

为了让在安装的时候这些特殊文件能被复制到``site-packages``下的文件夹中, 需要在``setup()``添加参数``include_package_data=True``.
In order for these files to be copied at install time to the package's folder inside ``site-packages``, you'll need to supply ``include_package_data=True`` to the ``setup()`` function.

.. note::

    添加在安装包中的文件(例如计算需要的数据文件)应该放在Python模块的文件夹里面(例如``funniest/funniest/data.json``).
    在加载这些文件的时候, 使用相对路径再加上``__file__``.
    Files which are to be used by your installed library (e.g. data files to support a particular computation method) should usually be placed inside of the Python module directory itself. E.g. in our case, a data file might be at ``funniest/funniest/data.json``. That way, code which loads those files can easily specify a relative path from the consuming module's ``__file__`` variable.
