组织更好地元数据
=======================

``setuptools.setup()`` 函数接受很多参数, 需要你填写关于你的包的元数据.
完整的填写这些参数可以让人们更加容易找到和判断你的包是干什么的.::

    from setuptools import setup

    setup(name='funniest',
          version='0.1',
          description='The funniest joke in the world',
          long_description='Really, the funniest around.',
          classifiers=[
            'Development Status :: 3 - Alpha',
            'License :: OSI Approved :: MIT License',
            'Programming Language :: Python :: 2.7',
            'Topic :: Text Processing :: Linguistic',
          ],
          keywords='funniest joke comedy flying circus',
          url='http://github.com/storborg/funniest',
          author='Flying Circus',
          author_email='flyingcircus@example.com',
          license='MIT',
          packages=['funniest'],
          install_requires=[
              'markdown',
          ],
          include_package_data=True,
          zip_safe=False)

``classifiers`` 参数, 完整的分类列表在这里 http://pypi.python.org/pypi?%3Aaction=list_classifiers.


README / Long Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~

你可能希望添加一个README说明文件到你的包中, 而且也可以满足PyPI ``long_description`` 的规范. 如果
这个文件使用reStructuredText语法, 将会有更丰富的格式.

**funniest**, 添加两个文件::

    funniest/
        funniest/
            __init__.py
        setup.py
        README.rst
        MANIFEST.in

``README.rst`` ::

    Funniest
    --------

    To use (with caution), simply do::

        >>> import funniest
        >>> print funniest.joke()

``MANIFEST.in`` ::

    include README.rst

这个文件是用来告诉setuptools打包的时候把README.rst添加进去, 否则的话只会打包包含Python代码的文件.

接下来修改 ``setup.py`` ::

    from setuptools import setup

    def readme():
        with open('README.rst') as f:
            return f.read()

    setup(name='funniest',
          version='0.1',
          description='The funniest joke in the world',
          long_description=readme(),
          classifiers=[
            'Development Status :: 3 - Alpha',
            'License :: OSI Approved :: MIT License',
            'Programming Language :: Python :: 2.7',
            'Topic :: Text Processing :: Linguistic',
          ],
          keywords='funniest joke comedy flying circus',
          url='http://github.com/storborg/funniest',
          author='Flying Circus',
          author_email='flyingcircus@example.com',
          license='MIT',
          packages=['funniest'],
          install_requires=[
              'markdown',
          ],
          include_package_data=True,
          zip_safe=False)

当你的代码存放在GitHub或者是BitBucket, README.rst 会自动成为项目的主页.