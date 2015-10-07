Specifying Dependencies
=======================

�����ʹ��Python, ����Ȼ�����ʹ����������PyPI���������ط����������İ�
If you're using Python, odds are you're going to want to use other public packages from PyPI or elsewhere.

setuptools�������ṩ�˺ܷ���Ĺ�����˵��������ϵ, �����ڰ�װ���ǵİ���ʱ����Զ���װ������.
Fortunately, setuptools makes it easy for us to specify those dependencies (assuming they are packaged correctly) and automatically install them when our packages is installed.

���Ǹ�**funniest** joke ���һЩ��ʽ�� ʹ��`Markdown <http://pypi.python.org/pypi/Markdown/>`_.
We can add some formatting spice to the **funniest** joke with `Markdown <http://pypi.python.org/pypi/Markdown/>`_.

``__init__.py``::

    from markdown import markdown

    def joke():
        return markdown(u'How do you tell HTML from HTML5?'
                        u'Try it out in **Internet Explorer**.'
                        u'Does it work?'
                        u'No?'
                        u'It's HTML5.')


�������ǵİ�����``markdown``�����. ������Ҫ��``setup.py``�����``install_requires``����::
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

Ϊ�˲����Ƿ���У����ǿ�����һ��``python setup.py develop``::
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

�����ǰ�װfunniest����ʱ��, ``pip install funniest``Ҳ��ͬʱ��װ``markdown``.
When we publish this to PyPI, calling ``pip install funniest`` or similar will also install ``markdown``.


����PyPI�еİ�
~~~~~~~~~~~~~~~~~~~~

��ʱ��, ����ҪһЩ����setuptools��ʽ��֯�İ�װ��, ��������û����PyPI����. �����������, �������``dependency_links``
���������ص�URL, ������Ҫ��URL�м�һЩ������Ϣ, setuptools������URL�ҵ��Ͱ�װ��Щ������.
Sometimes you'll want to use packages that are properly arranged with setuptools, but aren't published to PyPI.
In those cases, you can specify a list of one or more ``dependency_links`` URLs where the package can be downloaded,
along with some additional hints, and setuptools will find and install the package correctly.

�ٸ�����, Github�ϵİ����԰�������ĸ�ʽ��дURL::
For example, if a library is published on GitHub, you can specify it like::

    setup(
        ...
        dependency_links=['http://github.com/user/repo/tarball/master#egg=package-1.0']
        ...
    )
