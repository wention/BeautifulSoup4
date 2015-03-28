Beautiful Soup Documentation
============================

[Beautiful Soup](http://www.crummy.com/software/BeautifulSoup/) is a
Python library for pulling data out of HTML and XML files. It works
with your favorite parser to provide idiomatic ways of navigating,
searching, and modifying the parse tree. It commonly saves programmers
hours or days of work.

Quick Start
===========

Here's an HTML document I'll be using as an example throughout this
document. It's part of a story from `Alice in Wonderland`::

    html_doc = """
    <html><head><title>The Dormouse's story</title></head>
    <body>
    <p class="title"><b>The Dormouse's story</b></p>

    <p class="story">Once upon a time there were three little sisters; and their names were
    <a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
    <a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
    <a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
    and they lived at the bottom of a well.</p>

    <p class="story">...</p>
    """

Running the "three sisters" document through Beautiful Soup gives us a
``BeautifulSoup`` object, which represents the document as a nested
data structure::

    from bs4 import BeautifulSoup
    soup = BeautifulSoup(html_doc)

    print(soup.prettify())
    # <html>
    #  <head>
    #   <title>
    #    The Dormouse's story
    #   </title>
    #  </head>
    #  <body>
    #   <p class="title">
    #    <b>
    #     The Dormouse's story
    #    </b>
    #   </p>
    #   <p class="story">
    #    Once upon a time there were three little sisters; and their names were
    #    <a class="sister" href="http://example.com/elsie" id="link1">
    #     Elsie
    #    </a>
    #    ,
    #    <a class="sister" href="http://example.com/lacie" id="link2">
    #     Lacie
    #    </a>
    #    and
    #    <a class="sister" href="http://example.com/tillie" id="link2">
    #     Tillie
    #    </a>
    #    ; and they lived at the bottom of a well.
    #   </p>
    #   <p class="story">
    #    ...
    #   </p>
    #  </body>
    # </html>

Here are some simple ways to navigate that data structure::

    soup.title
    # <title>The Dormouse's story</title>

    soup.title.name
    # u'title'

    soup.title.string
    # u'The Dormouse's story'

    soup.title.parent.name
    # u'head'

    soup.p
    # <p class="title"><b>The Dormouse's story</b></p>

    soup.p['class']
    # u'title'

    soup.a
    # <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>

    soup.find_all('a')
    # [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
    #  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
    #  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]

    soup.find(id="link3")
    # <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>

One common task is extracting all the URLs found within a page's <a> tags::

    for link in soup.find_all('a'):
        print(link.get('href'))
    # http://example.com/elsie
    # http://example.com/lacie
    # http://example.com/tillie

Another common task is extracting all the text from a page::

    print(soup.get_text())
    # The Dormouse's story
    #
    # The Dormouse's story
    #
    # Once upon a time there were three little sisters; and their names were
    # Elsie,
    # Lacie and
    # Tillie;
    # and they lived at the bottom of a well.
    #
    # ...

Does this look like what you need? If so, read on.

Installing Beautiful Soup
=========================

If you're using a recent version of Debian or Ubuntu Linux, you can
install Beautiful Soup with the system package manager:

    $ apt-get install python-bs4`

Beautiful Soup 4 is published through PyPi, so if you can't install it
with the system packager, you can install it with ``easy_install`` or
``pip``. The package name is ``beautifulsoup4``, and the same package
works on Python 2 and Python 3.

    $ easy_install beautifulsoup4`

    $ pip install beautifulsoup4`

(The ``BeautifulSoup`` package is probably `not` what you want. That's
the previous major release, `Beautiful Soup 3`_. Lots of software uses
BS3, so it's still available, but if you're writing new code you
should install ``beautifulsoup4``.)

If you don't have ``easy_install`` or ``pip`` installed, you can
download the Beautiful Soup 4 source tarball
<http://www.crummy.com/software/BeautifulSoup/download/4.x/> and
install it with ``setup.py``.

    $ python setup.py install`

If all else fails, the license for Beautiful Soup allows you to
package the entire library with your application. You can download the
tarball, copy its ``bs4`` directory into your application's codebase,
and use Beautiful Soup without installing it at all.

I use Python 2.7 and Python 3.2 to develop Beautiful Soup, but it
should work with other recent versions.

