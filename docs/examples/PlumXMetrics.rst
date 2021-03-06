PlumX Metrics
-------------

:doc:`PlumXMetrics() <../reference/pybliometrics.PlumXMetrics>` implements the `PlumX Metrics API <https://dev.elsevier.com/documentation/PlumXMetricsAPI.wadl>`_.  It provides metrics in five categories: captures, citations, usage, mentions, and social media (`background information <https://plumanalytics.com/learn/about-metrics/>`_).  It works for 33 different types of media.

You initialize the class with the identifier of a document and its type:

.. code-block:: python
   
    >>> from pybliometrics.scopus import PlumXMetrics
    >>> plum = PlumXMetrics("10.1016/j.softx.2019.100263", id_type='doi')


You can obtain basic information just by printing the object:

.. code-block:: python

    >>> print(plum)
    Document with doi 10.1016/j.softx.2019.100263 has 105 citations in category 'capture'
    as of 2020-08-04, 3 citations in category 'citation', 1 citations in category
    'mention', 42 citations in category 'socialMedia', 4 citations in category 'usage'


To each of the five categories, there is one property storing number and origin of the metrics in `namedtuples <https://docs.python.org/3/library/collections.html#collections.namedtuple>`_.  If in a category there are no entries the property is simply `None`:

.. code-block:: python

    >>> >>> plum.capture
    [Metric(name='READER_COUNT', total=100),
     Metric(name='WATCHER_COUNT', total=3),
     Metric(name='FORK_COUNT', total=2)]
    >>> plum.citation
    [Metric(name='Scopus', total=3)]
    >>> plum.mention
    [Metric(name='ALL_BLOG_COUNT', total=1)]
    >>> plum.social_media
    [Metric(name='TWEET_COUNT', total=42)]
    >>> plum.usage
    [Metric(name='LINK_OUTS', total=3),
     Metric(name='ABSTRACT_VIEWS', total=1)]

Finally there is a property to total all metrics on an aggregated level:

.. code-block:: python

    >>> plum.category_totals
    [Category(name='capture', total=105),
     Category(name='citation', total=3),
     Category(name='mention', total=1),
     Category(name='socialMedia', total=42),
     Category(name='usage', total=4)]

There are no bibliometric information such as title or author.

Downloaded results are cached to speed up subsequent analysis.  This information may become outdated.  To refresh the cached results if they exist, set `refresh=True`, or provide an integer that will be interpreted as maximum allowed number of days since the last modification date.  For example, if you want to refresh all cached results older than 100 days, set `refresh=100`.  Use `source.get_cache_file_mdate()` to get the date of last modification, and `source.get_cache_file_age()` the number of days since the last modification.
