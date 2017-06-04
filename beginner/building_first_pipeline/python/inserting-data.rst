Populating the table
====================

A table with no content is really not too useful, so let's **populate** the ``Mouse`` table by inserting some data
manually. Let's explore a few different ways to insert data into the table, first one entry at a time,
and then multiple entries at once.

Inserting one entry at a time
-----------------------------

Let's first explore how you can enter new data, one row at a time.

Inserting a tuple/list
^^^^^^^^^^^^^^^^^^^^^^

You can insert a single entry (a single row in the table) as a Python *tuple* or *list*, with values in the order
of the attributes in the table:

.. code-block:: python

  mouse.insert1( (0, '2017-03-01', 'M') )

Here we used the table's ``insert1`` method to insert a new mouse with ``mouse_id`` of ``1``, ``dob``
(date of birth) of ``2017-03-01`` and ``gender`` ``M`` (male).

Verify the new entry by checking the table's content again:

.. code-block:: python

  >>> mouse
  *mouse_id    dob            gender
  +----------+ +------------+ +--------+
  0            2017-03-01     M
   (1 tuples)

Inserting a dictionary
^^^^^^^^^^^^^^^^^^^^^^

Alternatively you can first define a dictionary with attribute names as keys and fill the values.

.. code-block:: python
  
  data = {
    'mouse_id': 100,
    'dob': '2017-05-12',
    'gender': 'F'
  }

and then insert this dictionary into the table:

.. code-block:: python

  mouse.insert1(data)

Resulting in a new entry:

.. code-block:: python

  >>> mouse
  *mouse_id    dob            gender
  +----------+ +------------+ +--------+
  0            2017-03-01     M
  100          2017-05-12     F
   (2 tuples)

Inserting multiple entries at a time
------------------------------------

You can insert multiple entries at a time by passing in a list of tuples/list or dictionaries into the
talbe's ``insert`` method (that is, instead of ``insert1`` method). Let's prepare a few more mouse entries
and insert at once.

.. code-block:: python

  data = [
    (1, '2016-11-19', 'M'),
    (2, '2016-11-20', 'U'),
    (5, '2016-12-25', 'F')
  ]

  # now insert at once
  mouse.insert(data)

Verify the insert:

.. code-block:: python

  >>> mouse
  *mouse_id    dob            gender
  +----------+ +------------+ +--------+
  0            2017-03-01     M
  1            2016-11-19     M
  2            2016-11-20     U
  5            2016-12-25     F
  100          2017-05-12     F
   (5 tuples)

You can also do the same with a list of dictionaries:

.. code-block:: python

  data = [
    {'mouse_id': 10, 'dob': '2017-01-01', 'gender': 'F'},
    {'mouse_id': 11, 'dob': '2017-01-03', 'gender': 'F'},
  ]
  
  # insert them all
  mouse.insert(data)

This results in:

.. code-block:: python

  >>> mouse
  *mouse_id    dob            gender
  +----------+ +------------+ +--------+
  0            2017-03-01     M
  1            2016-11-19     M
  2            2016-11-20     U
  5            2016-12-25     F
  10           2017-01-01     F
  11           2017-01-03     F
  100          2017-05-12     F
   (7 tuples)

.. _duplicate-entry:

Data integrity
--------------
One of the key features of DataJoint is data integirty - a series of checks and restrictions to make sure that
our data remains consistent through its life in the data pipeline, and data integrity in DataJoint starts at data
entry!

For example, **data duplication** is prevented by checking and rejecting entries with already existing primary
key values. You can see this check in action by trying to insert a new entry with ``mouse_id`` that already exists
in the table!

.. code-block:: python

  >>> mouse.insert((0, '2015-03-03', 'U'))  # mouse with ---------------------------------------------------------------------------
  IntegrityError                            Traceback (most recent call last)
  <ipython-input-44-ce3dd3a7f75c> in <module>()
  ----> 1 mouse.insert1((0, '2015-03-03', 'U'))
  ...output truncated...
  IntegrityError: (1062, "Duplicate entry '0' for key 'PRIMARY'")

As you can see, trying to make a duplicate entries results in an ``IntegrityError``. As you step through the tutorial,
you will see more examples of how DataJoint ensures data integrity in the every step of the way but without
requiring much effort from your side! (aside from fixing problems when pointed out by DataJoint)

What's next?
------------
Now you have successfully entered some data into your first table, the data pipeline has some data to work
with! In the :doc:`next section <querying-data>` we will look at how to query and fetch data from your table!
