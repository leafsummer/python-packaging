��Ӳ��Դ���
==================

**funniest** ��ҪһЩ���Թ���. ��Щ���붼Ӧ�÷���``funniest.``��ģ���Ŀ¼��.
�����Ľṹ����Щ���Դ���ȿ��Ե���, �ֲ�����Ⱦȫ�ֵ������ռ�.::

    funniest/
        funniest/
            __init__.py
            tests/
                __init__.py
                test_joke.py
        setup.py
        ...

``test_joke.py`` �����ǵ�һ�������ļ�.
��Ȼ������һЩС�����, ��������Ϊ����ʾ�����������֯��, �������Ǵ�����``unittest.TestCase`` ��һ������::

    from unittest import TestCase

    import funniest

    class TestJoke(TestCase):
        def test_is_string(self):
            s = funniest.joke()
            self.assertTrue(isinstance(s, basestring))

������Щ����������õķ�ʽ��ʹ��`Nose <https://nose.readthedocs.org/en/latest/>`_ (�ر����㲻֪����ʲô��ʱ��)
The best way to get these tests going (particularly if you're not sure what to use) is `Nose <https://nose.readthedocs.org/en/latest/>`_. With those files added, it's just a matter of running this from the root of the repository::

    $ pip install nose
    $ nosetests

Ϊ�˰Ѳ��Թ������ɵ�``setup.py``��, ������Ҫ���һЩ����, ��Щ������ȷ�����в���������ʱ��Nose�ᱻ��װ.
To integrate this with our ``setup.py``, and ensure that Nose is installed when we run the tests, we'll add a few lines to ``setup()``::

    setup(
        ...
        test_suite='nose.collector',
        tests_require=['nose'],
    )

Ȼ��, ���ǾͿ����������в���::
Then, to run tests, we can simply do::

    $ python setup.py test

setuptools ���ᰲװnose�����в�������.
Setuptools will take care of installing nose and running the test suite.
