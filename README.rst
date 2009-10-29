==================
python-fiftystates
==================

Python library for interacting with the Fifty State Project API.

The Fifty State Project provides data on state legislative activities,
including bill summaries, votes, sponsorships and state legislator
information.

python-fiftystates is a project of Sunlight Labs (c) 2009.
Written by Michael Stephens <mstephens@sunlightfoundation.com>.

Source: http://github.com/sunlightlabs/python-fiftystates

Requirements
============

python >= 2.4

simplejson >= 1.8 (will use builtin json module instead on python >= 2.6)

Installation
============

To install run

    ``python setup.py install``

Usage
=====

Some examples:

    >>> import fiftystates
    >>> ca = fiftystates.State.get('ca')
    >>> print ca.name
    California
    >>> print ca.lower_chamber_name
    Assembly
    >>> for session in ca.sessions:
    ...     print session.name
    20092010
    20092010 Special Session 1
    20092010 Special Session 2
    20092010 Special Session 3
    20092010 Special Session 4

    >>> mikes = fiftystates.Legislator.search(state='ca', first_name='Mike')
    >>> for mike in mikes:
    ...     print mike.full_name
    Davis, Mike
    Eng, Mike
    Duvall, Mike D.
    Feuer, Mike

    >>> dem_mikes = fiftystates.Legislator.search(state='ca',
    ... party='Democrat', first_name='Mike')
    >>> for mike in dem_mikes:
    ...     print mike.full_name
    Davis, Mike
    Eng, Mike
    Feuer, Mike

    >>> bill = fiftystates.Bill.get('ca', '20092010', 'lower', 'AB20')
    >>> print bill.title
    An act to add Chapter 14.27 (commencing with Section 67325) to Part 40 of Division 5 of Title 3 of the Education Code, relating to public postsecondary education.

    >>> for sponsor in bill.sponsors:
    ...    print sponsor.full_name
    Solorio, Jose
    Block, Marty
    Portantino, Anthony
    Torlakson, Tom

    >>> for action in bill.actions[0:3]:
    ...     print action
    Senate (Committee CS61): Read second time, amended, and re-referred to Com. on  APPR.
    Senate (Floor Second Reading): From committee:  Amend, do pass as amended, and re-refer to Com. on  APPR.  (Ayes  5. Noes  0.) (June  23).
    Senate (Committee): From committee:  Do pass, and re-refer to Com. on  JUD. Re-referred.  (Ayes  8. Noes  0.) (June  10).

    >>> vote = bill.votes[0]
    >>> print vote.motion
    Do pass and be re-referred to the Committee on Appropriations.
    >>> print vote.yes_count, vote.no_count, vote.other_count
    7 3 0
