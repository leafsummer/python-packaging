如何打包你的Python代码
===============================

这个教程目标是为了更好地描述打包的过程，让大家都能学会如何打包Python代码。
但是打包并非**仅仅只有**一种方式，这个教程仅仅只描述了一种可行的打包方式。

打包之后，你的代码有如下好处:

* 可以使用 ``pip`` or ``easy_install`` 安装.
* 可以最为其他包的依赖关系.
* 其他用户更加方便地使用和测试你的代码.
* 其他用户可以更方便的理解你的代码，因为你的代码是按照打包需要的格式来组织的.
* 更加方便添加和分发文档.

我们一步一步地，制作一个简单的python包**funniest**，你就会发现我所说非虚。

.. toctree::
   :maxdepth: 1

   minimal
   dependencies
   metadata
   testing
   command-line-scripts
   non-code-files
   everything
   about

.. note::

   目前，这份教程仅仅针对Python 2.x，可能在Python 3.x 上并不适用

.. seealso::

    `Setuptools Documentation <http://pythonhosted.org/setuptools/>`_
        setuptools documentation.

    `Python Packaging User Guide <http://packaging.python.org>`_
        "Python Packaging User Guide" (PyPUG) 目标在于为Python包如何打包和安装，提供权威的指南.
