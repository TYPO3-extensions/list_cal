.. vim:set spell spelllang=en:

=============================================
List Calendar TYPO3 backend module (list_cal)
=============================================

This extension provides a backend module which lets you manage time-based database record in a calendar.

Usage
=====

After installation, you can use this extension right away to manage news records provided by extensions "news" nd "tt_news".
Just open the BE module "Web>List calendar" and chose a page on which you want to create, modify or view news records.

Configuration
=============

The extension is configured by TSconfig.

TSconfig properties
"""""""""""""""""""

Sub-keys of TSconfig path mod.web_listcal

.. container:: ts-properties

        ========================= ===============
        TSconfig property         Data type
        ========================= ===============
        newItemHour_              integer
        limitDaysOfWeek_          list
        table.[table].hideTable_  bool
        table.[table].dateColumn_ string
        ========================= ==============

.. _newItemHour:

newItemHour
~~~~~~~~~~~

Hour for new records create for a chosen day. ::

        # Example:
        # New created records will be created with a time of 7PM
        mod.web_listcal.newItemHour = 19

.. _limitDaysOfWeek:

limitDaysOfWeek
~~~~~~~~~~~~~~~

Limit display to some days of the week (0 = Sunday ... 6 = Saturday).

For example, you can include this on a page including your Wednesdays' events: ::

        # Example:
        # Show only wednesdays in the BE calendar:
        mod.web_listcal.limitDaysOfWeek = 3

.. _hideTable:

table.[table].hideTable
~~~~~~~~~~~~~~~~~~~~~~~

Do not show a certain table in the calendar. ::

        # Example:
        # Do not include tt_news on a page (page TSconfig) or for a certain user group (user TSconfig)
        mod.web_listcal.tables.tt_news.hideTable = 1

.. _dateColumn:

table.[table].dateColumn
~~~~~~~~~~~~~~~~~~~~~~~~

Enable support for a certain table by specifying a field which holds a timestamp.
For example you can add support for :code:`list_cal` to your TYPO3 extension by putting this to your :code:`ext_tables.php`: ::

        // Add support for TYPO3 extension "list_cal" to my cool extension
        // by adding database field `startDate` to their configuration:
        t3lib_extMgm::addPageTSConfig('
                mod.web_listcal.table {
                        tx_myext_domain_model_mytable {
                                dateColumn = startDate
                        }
                }
        }');