.. image:: ./logo.png
===========================

.. image:: https://badge.fury.io/py/clippercard.png
    :target: http://badge.fury.io/py/clippercard

.. image:: https://pypip.in/d/clippercard/badge.png
        :target: https://crate.io/packages/clippercard/
        
.. image:: https://pypip.in/license/vxapi/badge.png
        :target: ./LICENSE

``clippercard`` is an unofficial web API to clippercard.com, written in Python.


Why
---

Not only is the `clippercard web site <https://www.clippercard.com>`_ a total UX/UI disaster, its behind-the-scene's HTML structure and HTTP protocol is a complete exercise in palmface. This library aims to provide an unofficial but sensible interface to the official web service.

Project Goal
------------

I enjoy the actual user experience of ClipperCard on buses and trains. My complaints about the service are purely isolated to its web interface. I saw a problem, and I solved it for myself, that's all.

As an advocate for data accessibility, I believe our dollars, our votes, our voices and our actions can nudge institutions in the direction we'd like them to go. At Bay Area's `Metropolitan Transportation Commission <http://www.mtc.ca.gov/about_mtc/staff_contacts.htm>`_, I am sure there are a lot of great people doing good work to the best of their ability, and within the context of prioritization, organizational structure and resources available to them.

I encourage the staff of MTA reading this project to see this effort as a nudge for a public and official API. The moment they put up an API that obsoletes this project, I will happily direct followers to the official solution. If you'd like them to increase attention to data accessibility, you can send them an email at info@mtc.ca.gov and tell them I sent you.

If you'd like to see more development, you can `support this project on Gittip <https://www.gittip.com/anthonywu/>`_

Features
--------

- Profile Data
- Multiple cards' data
- For each card, multiple products and balances

I don't have access to all products loadable on the ClipperCard, so transit product variant support is limited to what I personally use for now. If you'd like me to add support for your product, send me the page source from your `account home page <https://www.clippercard.com/ClipperCard/dashboard.jsf>`_

Security and Privacy
--------------------

It's important to point out that:

- This project does not collect your personal information or clippercard.com login credentials.
- This project is not a hosted service, your data is not stored or sent to any 3rd party service.

For now, this project is targeted at other software developers, who are capable of assessing my source code for security implications.


Installation
------------

To install clippercard, simply:

.. code-block:: bash

    $ pip install clippercard

Usage
-----

.. code-block:: python

    import clippercard
    session = clippercard.Session(<username>, <password>)
    print(session.user_profile)
    for c in session.cards:
        print(c)


You also get a super convenient command line binary ``clippercard``::


    $ clippercard -h # see usage information

    $ clippercard summary

    +---------+-------------------------------------------+
    |    name | ANTHONY WU                                |
    |   email | anthonywu@example.com                     |
    | address | 1 Main St, San Francisco, CA 94103        |
    |   phone | 415-555-5555                              |
    +---------+-------------------------------------------+
    +---------------+------------+-------+--------+----------------+--------+
    | Card          | Serial     | Type  | Status | Product        | Value  |
    +---------------+------------+-------+--------+----------------+--------+
    | GGB75         | 1234567890 | ADULT | Active | BART HVD 60/64 | $16.20 |
    | GGB75         | 1234567890 | ADULT | Active | Cash value     | $32.40 |
    | Standard Card | 1234567891 | ADULT | Active | Cash value     | $64.80 |
    +---------------+------------+-------+--------+----------------+--------+


If you wish to use clippercard without specifying username/password on the CLI, create a file ``~/.clippercardrc`` with this format::

    [default]
    username = anthonywu@example.com
    password = superseekrit

You may toggle accounts via the ``--account`` flag on the command line to access one of several configs in the file::

    [default]
    username = <replace_with_your_email>
    password = <replace_with_your_password>
    
    [wife]
    username = <replace_with_login_email>
    password = <replace_with_login_password>
    
The ``wife`` credentials can then be accessed via::

    $ clippercard summary --account=wife

Contribute
----------

#. fork the repo
#. make your changes
#. follow local style consistency, then PEP8
#. run pyflakes/frosted on your diffs
#. add unit tests, make sure they pass =)
#. send me a pull request w/ explanation of design decisions
