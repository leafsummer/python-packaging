添加测试代码
==================

**funniest** 需要一些测试工作. 这些代码都应该放在 ``funniest.`` 子模块的目录下.
这样的结构，这些测试代码既可以导入, 又不会污染全局的命名空间.::

    funniest/
        funniest/
            __init__.py
            tests/
                __init__.py
                test_joke.py
        setup.py
        ...

``test_joke.py`` 是我们第一个测试文件.
虽然现在有一些小题大做, 但是这是为了演示代码是如何组织的, 所以我们创建了 ``unittest.TestCase`` 的一个子类::

    from unittest import TestCase

    import funniest

    class TestJoke(TestCase):
        def test_is_string(self):
            s = funniest.joke()
            self.assertTrue(isinstance(s, basestring))

运行这些测试用例最好的方式是使用 `Nose <https://nose.readthedocs.org/en/latest/>`_  (特别是你不知道用什么的时候)

    $ pip install nose
    $ nosetests

为了把测试工作集成到 ``setup.py`` 中, 我们需要添加一些参数, 这些参数会确保运行测试用例的时候Nose会被安装.::

    setup(
        ...
        test_suite='nose.collector',
        tests_require=['nose'],
    )

然后, 我们就可以这样运行测试::

    $ python setup.py test

setuptools 将会安装nose和运行测试用例.