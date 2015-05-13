helga-facts
===========

A helga plugin that can be used to store responses that can be returned from a question. For example::

    <sduncan> foo is bar
    <sduncan> foo?
    <helga> foo is bar (sduncan on 12/01/2014 08:15)
    <sduncan> bar baz are qux
    <sduncan> bar baz?
    <helga> bar baz is qux (sduncan on 12/01/2014 08:15)

Facts are queried using the form ``fact?`` and are stored automatically using the form
``fact (is|are) term``. In this simple fact storing form, facts are saved with the nick of the user
that saying it and the timestamp at which it was said. Facts can also be stored as a reply only
without a nick or timestamp by using the token '<reply>'::

    <sduncan> foo is <reply> bar
    <sduncan> foo?
    <helga> bar

Optionally, if the setting ``FACTS_REQUIRE_NICKNAME`` is set to True, the bot's nick will be required
to show a stored fact::

    <sduncan> foo is <reply> bar
    <sduncan> foo?
    <sduncan> helga foo?
    <helga> bar

.. important::

    This plugin requires database access

Fact storage tends to be a bit greedy at times, since the form of a fact is ``fact (is|are) term``. This
can lead to situations where you may see one-word pronoun facts that can be annoying. For example::

    <sduncan> who is going to the party?
    <sduncan> who?
    <helga> who is going to the party? (sduncan on 12/01/2014 08:15)

For this reason, you can customize the setting ``FACTS_WORD_BLACKLIST``, which should be a list of words
that will result in a fact being stored. Generally this will be pronouns. The default value for this is::

    FACTS_WORD_BLACKLIST = ['who', 'what', 'where', 'why', 'how']

Note that this only occurs for facts that do not include ``<reply>``. This will still work::

    <sduncan> when is <reply> now
    <sduncan> when?
    <helga> now


License
-------

Copyright (c) 2015 Shaun Duncan

Licensed under an `MIT`_ license.

.. _`MIT`: https://github.com/shaunduncan/helga-facts/blob/master/LICENSE
