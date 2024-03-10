BarrelDB documentation
-----------------------------

SETUP 
=============

``INV_init()``
~~~~~~~~~~~~~
Defines the global variables and constants which the database system uses.

IMPORTANT:
++++++++++
This must be run every time the plot restarts

Please do not manually modify any of the globals outside of this function

Modifying the existing globals at all is not recommended. Doing so is at your own risk!

FINDING, RESERVING, AND CLEARING
================================

``INV_findFreeSpace(result: var, slots: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Looks for the first available place that can store {slots}, and stores the output index in {result}

``INV_rsvSpace(index: num, slots: num, reserverType: str)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Reserves a space at {index}, for {slots}, with the specified {reserverType}

``INV_findAndReserve(index: var, size: num, reserverType: str)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Looks for the first available place that can store {size} slots, reserves it with the specified {reserverType}, and stores the control item's index in {index} 

NOTE: This function is a combination of INV_findFreeSpace and INV_rsvSpace.

``INV_markAsFree(index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Marks the item at {index} as free (not taken)
NOTE: If the function fails for any reason (item already free, incorrect item type, etc.), It will not perform any changes.

ITEM MANIPULATION
=================

``INV_getItemAtIndex(result: var, index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gets the item at {index}, and stores it in {result}

``INV_getItemsAtIndexes(result: var, startIndex: num, endIndex: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Returns a list of the items between {startIndex} and {endIndex} to {result}

``INV_setItemAtIndex(item: item, index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sets the item at {index} to {item}

``INV_setItemsAtIndex(items: item(s), index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Adds all {items} in the list sequentially, one after another, starting with the first item at the spacified {index}

``INV_getItemTags(result: var, item: item)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Dumps an {item}' s tags to a dictionary, and stores it in {result}
                                            
**TIP:** This is useful for modifying Control Items

``INV_setItemTags(result: var, item: item, tags: dict)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sets an {item}' s {tags}, and stores the {result}

**TIP:** This is useful for modifying Control Items

``INV_getItemTagsAtIndex(result: var, index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gets the item at {index}, and saves its tags to {result}

``INV_setItemtagsAtIndex(tags: dict, index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gets the item at {index}, and sets its {tags}

``INV_getReserverItems(result: var, index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Gets all the items a reserver, that is in {index}, is reserving, and stores the {result}.

EXAMPLE:
++++++++
::
  
        1  2     3  4  5  6  7  8
  db : [G, R(5), A, B, C, D, E, F]
  
  INV_getReserverItems(items, 2) # items = [A, B, C, D, E]


REAL-WORLD VALUES
=================

``INV_getIndex(result: var, brlLoc: loc, brlIndex: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Converts {brlLoc} and {brlIndex} to the matching database index, and stores the {result}

``INV_getIndexBrl(result: var, index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Converts the database {index} to the real-world location of the barrel, and stores the {result}

``INV_getIndexBrlIndex(result: var, index: num)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Converts the db {index} to the real-world index within the barrel, and stores the {result}

UTILS
=====
``INV_getDBSize(result: var)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Returns the db's size (in slots) to {result}
