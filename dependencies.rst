Specifying Dependencies
=======================

如果你使用Python, 很自然的你会使用其他人在PyPI或者其他地方公开发布的包
If you're using Python, odds are you're going to want to use other public packages from PyPI or elsewhere.

setuptools给我们提供了很方便的工具来说明依赖关系, 而且在安装我们的包的时候回自动安装依赖包.
Fortunately, setuptools makes it easy for us to specify those dependencies (assuming they are packaged correctly) and automatically install them when our packages is installed.

我们给**funniest** joke 添加一些格式， 使用`Markdown <http://pypi.python.org/pypi/Markdown/>`_.
We can add some formatting spice to the **funniest** joke with `Markdown <http://pypi.python.org/pypi/Markdown/>`_.

``__init__.py``::

    from markdown import markdown

    def joke():
        return markdown(u'How do you tell HTML from HTML5?'
                        u'Try it out in **Internet Explorer**.'
                        u'Does it work?'
                        u'No?'
                        u'It's HTML5.')


现在我们的包依赖``markdown``这个包. 我们需要在``setup.py``中添加``install_requires``参数::
Now our package depends on the ``markdown`` package. To note that in ``setup.py``, we just add an ``install_requires`` keyword argument::

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

为了测试是否可行，我们可以试一试``python setup.py develop``::
To prove this works, we can run ``python setup.py develop`` again, and we'll see::

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

当我们安装funniest包的时候, ``pip install funniest``也会同时安装``markdown``.
When we publish this to PyPI, calling ``pip install funniest`` or similar will also install ``markdown``.


不在PyPI中的包
~~~~~~~~~~~~~~~~~~~~

有时候, 你需要一些按照setuptools格式组织的安装包, 但是它们没有在PyPI发布. 在这种情况下, 你可以在``dependency_links``
中填入下载的URL, 可能需要在URL中加一些其他信息, setuptools将根据URL找到和安装这些依赖包.
Sometimes you'll want to use packages that are properly arranged with setuptools, but aren't published to PyPI.
In those cases, you can specify a list of one or more ``dependency_links`` URLs where the package can be downloaded,
along with some additional hints, and setuptools will find and install the package correctly.

举个例子, Github上的包可以按照下面的格式填写URL::
For example, if a library is published on GitHub, you can specify it like::

    setup(
        ...
        dependency_links=['http://github.com/user/repo/tarball/master#egg=package-1.0']
        ...
    )
