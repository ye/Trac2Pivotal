Trac Ticket to Pivotal CSV Converter
====================================

A very simple script to convert [Trac][] tickets to a CSV-file importable by
[Pivotal Tracker][].


Warning: Don't blame me
-----------------------

This is intended as a starting point for a migration from a customized Trac.
You may use it as base for your own implementation, play with it, fork it and
if you extend it I'll be very pleased to receive pull requests.

But I'm not reponsible if you use it and anything happens that you don't like,
expected or not.


Features
--------

* imports all ticket as stories
* keeps summary, description, time created, time changed, owner, reporter
* components and keywords and version and milestone become labels (a.k.a. tags)
* translates ticket status and resolution to story state and estimate
* translates ticket type to story type
* for reference the ticket number is added to the story ("Add some karma (Trac
  Ticket #23)")
* easily customizable by editing the source code


Bugs / Enhancements / Comments
------------------------------

Please feel free to provide feedback, bug reports and enhancement requests via
the [Github issue tracker][ghi]


Known Bugs / Limitations
------------------------

* severity, cc, priority are lost
* most Trac formatting (lists, links etc.) is neither translated nor
  supported
* Ticket references ("#23") are not updated since the ID of the new Ticket is
  not known in advance. This could be solved by using the HTTP API instead of
  CSV file import.
* Mapping between states is generally difficult since both systems follow
  very different routes. For example "wontfix" or "invalid" in Trac don't have
  a correspondent state in Pivotal Tracker.

To Do
-----

 * support porting notes timestamps


Installation
------------

Requirements: Python (tested with 2.7)

As Trac allows modification of state, resolution etc. and most probably your
users won't be named equal in Trac and Pivotal, you may want to modify the
source, especially these:

* `STATES`: Converts ticket state and resolution to story state and estimate
  (points).
* `TYPES`: Converts ticket type to story type.
* `format_story()`: Adds the Trac ticket number to the story.
* `translate_user()`: Converts user names (fill in your own data).


Usage
-----

    ./trac2pivotal.py trac.db mytractickets.csv

It probably is a good idea to manually inspect the resulting CSV file and
perhaps test one or two of the lines that look like they most likely won't
work (they usually do, spoiling your expectation).

If you can't seem to find the tickets in Pivotal Tracker they might just be
too old to be shown in the history. Try increasing the "Number of Done
Iterations to Show" in the project settings to make them appear.


[Trac]: http://trac.edgewall.org
[Pivotal Tracker]: https://www.pivotaltracker.com
[ghi]: https://github.com/hinnerk/Trac2Pivotal/issues