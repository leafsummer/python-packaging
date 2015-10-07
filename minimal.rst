��С�Ľṹ
=================

����������һС�δ���::

    def joke():
        return (u'�������HTML��HTML5?'
                u'��IE������,�������������ʾ����HTML5')

��С�δ��������Ϊ��չʾ��δ���ͷַ�Python���롣


ѡ��һ������
~~~~~~~~~~~~~~

Python ģ����߰���Ӧ���������µĹ���:
Python module/package names should generally follow the following constraints:

* ȫСд
* ��Ҫ��pypi�����еİ����ظ�����ʹ�㲻�빫��������İ�����Ϊ��İ�������Ϊ��������������
* ʹ���»��߷ָ����ʻ���ʲô������(��Ҫʹ�����ַ�)

���ڰ����ǵĺ������һ��Python module **funniest**


��ʼ����
~~~~~~~~~~~~~~~~~~~~~~~~

Ŀ¼�ṹ **funniest** ����::

    funniest/
        funniest/
            __init__.py
        setup.py

������Ŀ¼�����ǰ汾�����ߵĸ�Ŀ¼, ����``funniest.git``. ��Ŀ¼��Ҳ��``funniest``, ����Python module.

Ϊ�˸������, ���ǰѺ���``joke()`` �ŵ� ``__init__.py``��::

    def joke():
        return (u'�������HTML��HTML5?'
                u'��IE������,�������������ʾ����HTML5')

����Ҫ��setup�����ļ���``setup.py``, Ӧ�ð���һ�д������``setuptools.setup()``,������������::

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

�������ǿ����ڱ��ذ�װ���python��::

    $ python setup.py install

����Ҳ����ʹ�ÿ���ģʽ��װ�����, ÿ���޸Ĵ���֮�������°�װ, �����������µĴ���.

    $ python setup.py develop

���������ַ�ʽ����װ֮��Ϳ�����python��ʹ�������::

    >>> import funniest
    >>> print funniest.joke()


��PyPI�Ϸ���
~~~~~~~~~~~~~~~~~~

�ű� ``setup.py`` Ҳ����PyPIע����ϴ�Դ��������.
``setup.py`` script is also our main entrypoint to register the package name on PyPI and upload source distributions.

��һ��ע�������(����ע�����,�ϴ�Ԫ����,����pypi.python.org��ҳ��)::

    $ python setup.py register

�����δ��PyPI�Ϸ���������, ����Ҫ����һ���˺�, �������򵼻�һ��һ����������ô��.
If you haven't published things on PyPI before, you'll need to create an account by following the steps provided at this point.

ע��֮���������PyPI�����������ҳ��**funniest**:
At this point you can view the (very minimal) page on PyPI describing **funniest**:

http://pypi.python.org/pypi/funniest/0.1

�����û����Ը���URL�����ҵ����git�ֿ�, ����Ϊ��ʹ�÷���������Ҫ�ϴ�һ��Դ���. �û�����Ҫclone���git�ֿ⣬���ҿ���ʹ�ð�װ����
�Զ�����װ������������ϵ.
Although users can follow the URL link to find our git repository, we'll probably want to upload a source distribution so that the package can be installed without cloning the repository. This will also enable automated installation and dependency resolution tools to install our package.

�ڶ�������һ��Դ���::
First create a source distribution with::

    $ python setup.py sdist

��һ��������Ķ���Ŀ¼�´���``dist/funniest-0.1.tar.gz``. �������ʱ��, ���԰�����ļ���������һ̨������, ��ѹȻ��װ,
����һ�°�װ��.
This will create ``dist/funniest-0.1.tar.gz`` inside our top-level directory. If you like, copy that file to another host and try unpacking it and install it, just to verify that it works for you.

�������ϴ���PyPI::
That file can then be uploaded to PyPI with::

    $ python setup.py sdist upload

����԰��⼸���������, ����Ԫ����, �����°汾, һ�������::
You can combine all of these steps, to update metadata and publish a new build in a single step::

    $ python setup.py register sdist upload

��Ҫ�鿴setup.py����Ĺ��ܿ��Կ�������::
For a detailed list of all available setup.py commands, do::

    $ python setup.py --help-commands


��װ�����
~~~~~~~~~~~~~~~~~~~~~~

����Ĳ������֮��, �����û�����ֱ����``easy_install``��װ::
At this point, other consumers of this package can install the package with ``easy_install``::

    easy_install funniest

����ʹ��``pip``::
Or better yet, ``pip``::

    $ pip install funniest

��������Ϊ��������������, �������Զ���װ(�����ں�����ᵽ�������)
They can specify it as a dependency for another package, and it will be automatically installed when that package is installed (we'll get to how to do that later).


��������ļ�
~~~~~~~~~~~~~~~~~~~~~~~

�󲿷�ʱ�����ǵĴ����ɢ�ڶ���ļ�����,
Most of the time we'll want more than one file containing code inside of our module. Additional files should always be added inside the inner ``funniest`` directory.

�ٸ�����, ���ǰѺ����ƶ���һ���µ��ļ���``text``, �������ǵ�Ŀ¼�ṹ�������ӵ�::
For example, let's move our one function to a new ``text`` submodule, so our directory hierarchy looks like this::

    funniest/
        funniest/
            __init__.py
            text.py
        setup.py

``__init__.py``::

    from .text import joke

``text.py``::

    def joke():
        return (u'�������HTML��HTML5?'
                u'��IE������,�������������ʾ����HTML5')

���еĴ���Ӧ�ö��� ``funniest/funniest/`` Ŀ¼��.


���Ե��ļ� (.gitignore, etc)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

���ǿ�����Ҫһ��``.gitignore``�ļ�, ��Ϊ�������Ĺ����л����һ���м��ļ�, ���ǲ������ύ������ֿ⵱��.
������һ��``.gitignore``������::
There's one more thing we'll probably want in a 'bare bones' package: a ``.gitignore`` file, or the equivalent for other SCMs. The Python build system creates a number of intermediary files we'll want to be careful to not commit to source control. Here's an example of what ``.gitignore`` should look like for **funniest**::

    # Compiled python modules.
    *.pyc

    # Setuptools distribution folder.
    /dist/

    # Python egg metadata, regenerated from source files by setuptools.
    /*.egg-info


�󹦸��
~~~~~~~~~~~~~~~~~~~

���潲�Ľṹ�Ѿ������˴���һ���������в���. ������е�Python���ߺͿⶼ��ѭͬ���Ĺ��������, ������������.
The structure described so far is all that's necessary to create reusable simple packages with no 'packaging bugs'. If every published Python tool or library used followed these rules, the world would be a better place.

**�͹ٱ�** ���滹�и�������, ��Ϊ�󲿷ֵİ�����Ҫ�����нű�, �ĵ�, ���ԣ��������ߵȵ�, �뿴��һƪ.
**But wait, there's more!** Most packages will want to add things like command line scripts, documentation, tests, and analysis tools. Read on for more.
