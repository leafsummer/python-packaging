依赖关系
=======================

如果你使用Python, 很自然的你会使用其他人在PyPI或者其他地方公开发布的包

setuptools给我们提供了很方便的工具来说明依赖关系, 而且在安装我们的包的时候会自动安装依赖包.

我们可以给 **funniest** joke 添加一些格式， 使用 `Markdown <http://pypi.python.org/pypi/Markdown/>`_.

``__init__.py`` ::

    from markdown import markdown

    def joke():
        return markdown(u'How do you tell HTML from HTML5?'
                        u'Try it out in **Internet Explorer**.'
                        u'Does it work?'
                        u'No?'
                        u'It\'s HTML5.')


现在我们的包依赖 ``markdown`` 这个包. 我们需要在 ``setup.py`` 中添加 ``install_requires`` 参数::

    from setuptools import setup

    setup(name='funniest',
          version='0.1',
          description='The funniest joke in the world',
          url='http://github.com/storborg/funniest',
          author='Flying Circus',
          author_email='flyingcircus@example.com',
          license='MIT',
          packages=['funniest'],
          install_requires=[
              'markdown',
          ],
          zip_safe=False)

为了测试是否可行，我们可以试一试 ``python setup.py develop`` ::

    $ python setup.py develop
    running develop
    running egg_info
    writing requirements to funniest.egg-info/requires.txt
    writing funniest.egg-info/PKG-INFO
    writing top-level names to funniest.egg-info/top_level.txt
    writing dependency_links to funniest.egg-info/dependency_links.txt
    reading manifest file 'funniest.egg-info/SOURCES.txt'
    writing manifest file 'funniest.egg-info/SOURCES.txt'
    running build_ext
    Creating /.../site-packages/funniest.egg-link (link to .)
    funniest 0.1 is already the active version in easy-install.pth

    Installed /Users/scott/local/funniest
    Processing dependencies for funniest==0.1
    Searching for Markdown==2.1.1
    Best match: Markdown 2.1.1
    Adding Markdown 2.1.1 to easy-install.pth file

    Using /.../site-packages
    Finished processing dependencies for funniest==0.1

当我们安装funniest包的时候, ``pip install funniest`` 也会同时安装 ``markdown`` .


不在PyPI中的包
~~~~~~~~~~~~~~~~~~~~

有时候, 你需要一些按照setuptools格式组织的安装包, 但是它们没有在PyPI发布. 在这种情况下, 你可以在 ``dependency_links``
中填入下载的URL, 可能需要在URL中加一些其他信息, setuptools将根据URL找到和安装这些依赖包.

举个例子, Github上的包可以按照下面的格式填写URL::

    setup(
        ...
        dependency_links=['http://github.com/user/repo/tarball/master#egg=package-1.0']
        ...
    )
