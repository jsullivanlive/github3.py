github3.py
==========

.. image::
    https://secure.travis-ci.org/sigmavirus24/github3.py.png?branch=master
    :alt: Build Status
    :target: http://travis-ci.org/sigmavirus24/github3.py

Eventually this will be a python module to access the GitHub v3 API.

This is not stable yet and there is no backwards compatibility yet. There will 
likely be some changes which change behavior in the near future.

Installation
------------

::

    $ pip install github3.py

Dependencies
------------

- requests_  by Kenneth Reitz
  
.. _requests: https://github.com/kennethreitz/requests

License
-------

Modified BSD license_

.. _license:

Examples
--------

See the docs_ for more detailed examples.

.. _docs: http://github3py.readthedocs.org/en/latest/index.html#more-examples

::

  >>> from github3 import login
  >>> gh = login(username, password)
  >>> issue = gh.issue('sigmavirus24', 'Todo.txt-python', 17)
  >>> issue.html_url
  u'https://github.com/sigmavirus24/Todo.txt-python/issues/17'
  >>> issue.state
  u'open'
  >>> events = issue.list_events()
  >>> events
  [<Issue Event [#17 - subscribed - sigmavirus24]>, <Issue Event [#17 - assigned - sigmavirus24]>,
   <Issue Event [#17 - referenced - sigmavirus24]>]
  >>> events[0].actor
  <User [sigmavirus24:None]>
  >>> events[0].issue
  <Issue [sigmavirus24/Todo.txt-python #17]>
  >>> events[0].closed_at
  >>> events[0].event
  u'subscribed'

::

  >>> from github3 import login
  >>> g = login(username, password)
  >>> repo = g.repository('sigmavirus24', 'Todo.txt-python')
  >>> sha = repo.create_blob('Testing blob creation', 'utf-8')
  >>> sha
  u'57fad9a39b27e5eb4700f66673ce860b65b93ab8'
  >>> blob = repo.blob(sha)
  >>> blob.content
  u'VGVzdGluZyBibG9iIGNyZWF0aW9u\n'
  >>> blob.decoded
  u'Testing blob creation'
  >>> blob.encoding
  u'base64'

::

  >>> from github3 import login
  >>> g = login(username, password)
  >>> repo = g.repository('sigmavirus24', 'github3.py')
  >>> tag = repo.tag('cdba84b4fede2c69cb1ee246b33f49f19475abfa')
  >>> tag
  <Tag [cdba84b4fede2c69cb1ee246b33f49f19475abfa]>
  >>> tag.object.sha
  u'24ea44d302c6394a0372dcde8fd8aed899c0034b'
  >>> tag.object.type
  u'commit'

Contributing
------------

Please see the section_ of the documentation pertaining to this.

Testing
~~~~~~~

If you want to run the unittests with authentication, simply run::

    make alltests

From the root of the repository. If you would rather see what will take place 
on Travis, run::

    make travis
    # or
    make tests


.. links
.. _section: http://github3py.readthedocs.org/en/latest/index.html#contributing

Author
------

Ian Cordasco (sigmavirus24)

Contact Options
---------------

- You may contact (via email) the author directly with questions/suggestions
- You may send your email to github3.py@librelist.com
