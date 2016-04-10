udon: a distributed static file web server
=============================

Udon is a static file web service, generally intended to be used at the edge of a network to serve static assets for websites like CSS files, javascript, images or other content which does not change frequently or is dynamically part of the web application state.

It's also built on top of [riak_core][0] and provides a simple application which is intended to introduce the kinds of programming that's required to implement a riak_core application including handoff logic between vnodes.  I wrote this as a tool to teach for [Erlang Factory SF 2015][1].

Slides and video
----------------
The slides can be found [on SpeakerDeck][2].

The video for the talk is available [on YouTube][3].

[0]: https://github.com/basho/riak_core
[1]: http://www.erlang-factory.com/sfbay2015/mark-allen
[2]: https://speakerdeck.com/mrallen1/building-distributed-applications-with-riak-core 
[3]: https://www.youtube.com/watch?v=LKsNbYf9mLw

Building
--------
Make sure you have Erlang 17+ installed and operational. You also will need a working C++ compiler and GNU make.  Clone the repo.

    $ cd udon 
    $ make devrel
  
Building a cluster
------------------

    $ for d in dev/*; do $d/bin/udon start; done
    $ dev/dev2/bin/udon-admin cluster join udon1@127.0.0.1
    $ dev/dev3/bin/udon-admin cluster join udon1@127.0.0.1
    $ dev/dev4/bin/udon-admin cluster join udon1@127.0.0.1
    $ dev/dev1/bin/udon-admin cluster plan
    $ dev/dev1/bin/udon-admin cluster commit
    $ dev/dev1/bin/udon-admin member-status

Running
-------

    $ dev/dev1/bin/udon attach
    udon1@127.0.0.1:1> udon:store("test", <<"foo">>).
  
