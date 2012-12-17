Changelog
=========

11 (2012-12-16)
---------------

- Add optional support for socket.getfqdn. [Jeremy Kitchen]

  For my setup I need to have the fqdn used at all times since my
  hostnames are the same but the environment (among other things) is
  found in the rest of the FQDN.
  
  Since just changing socket.gethostname to socket.getfqdn has lots of
  potential for breakage, and socket.gethostname doesn't always return
  an
  FQDN, it's now an option to explicitly always use the fqdn.
  
  Fixes #68

- Check for log file truncation fixes #55. [Jeremy Kitchen]

  This adds a simple check for log file truncation and resets the watch
  when detected.
  
  There do exist 2 race conditions here:
  1. Any log data written prior to truncation which beaver has not yet
  read and processed is lost. Nothing we can do about that.
  2. Should the file be truncated, rewritten, and end up being larger
  than
  the original file during the sleep interval, beaver won't detect
  this. After some experimentation, this behavior also exists in GNU
  tail, so I'm going to call this a "don't do that then" bug :)
  
  Additionally, the files beaver will most likely be called upon to
  watch which may be truncated are generally going to be large enough
  and slow
  filling enough that this won't crop up in the wild.

- Add a version number to beaver. [Jose Diaz-Gonzalez]

10 (2012-12-15)
---------------

- Fixed package name. [Jose Diaz-Gonzalez]

- Regenerate CHANGES.rst on release. [Jose Diaz-Gonzalez]

- Adding support for /path/{foo,bar}.log. [Josh Braegger]

- Ignore file errors in unwatch method -- the file might not exists.
  [Josh Braegger]

- Unwatch file when encountering a stale NFS handle. When an NFS file
  handle becomes stale (ie, file was removed), it was crashing beaver.
  Need to just unwatch file. [Josh Braegger]

- Consistency. [Chris Faulkner]

- Pull install requirements from requirements/base.txt so they don't get
  out of sync. [Chris Faulkner]

- Include changelog in setup. [Chris Faulkner]

- Convert changelog to RST. [Chris Faulkner]

- Actually show the license. [Chris Faulkner]

- Consistent casing. [Chris Faulkner]

- Consistency. [Chris Faulkner]

- Stating the obvious. [Chris Faulkner]

- Grist for the mill. [Chris Faulkner]

- Drop redundant README.txt. [Chris Faulkner]

- Don't use empty string for tag when no tags configured in config file.
  [Stylianos Modes]

- Making 'mode' option work for zmqtransport.  Adding setuptools and
  tests (use ./setup.py nosetests).  Adding .gitignore. [Josh Braegger]

9 (2012-11-28)
--------------

- More release changes. [Jose Diaz-Gonzalez]

- Fixed deprecated warning when declaring exchange type. [Rafael
  Fonseca]

7 (2012-11-28)
--------------

- Added a helper script for creating releases. [Jose Diaz-Gonzalez]

- Partial fix for crashes caused by globbed files. [Jose Diaz-Gonzalez]

- Removed deprecated usage of e.message. [Rafael Fonseca]

- Fixed exception trapping code. [Rafael Fonseca]

- Added some resiliency code to rabbitmq transport. [Rafael Fonseca]

6 (2012-11-26)
--------------

- Fix issue where polling for files was done incorrectly. [Jose Diaz-
  Gonzalez]

- Added ubuntu init.d example config. [Jose Diaz-Gonzalez]

5 (2012-11-26)
--------------

- Try to poll for files on startup instead of throwing exceptions.
  Closes #45. [Jose Diaz-Gonzalez]

- Added python 2.6 to classifiers. [Jose Diaz-Gonzalez]

4 (2012-11-26)
--------------

- Remove unused local vars. [Jose Diaz-Gonzalez]

- Allow rabbitmq exchange type and durability to be configured. [Jose
  Diaz-Gonzalez]

- Remove unused import. [Jose Diaz-Gonzalez]

- Formatted code to fix PEP8 violations. [Jose Diaz-Gonzalez]

- Use alternate dict syntax for Python 2.6 support. Closes #43. [Jose
  Diaz-Gonzalez]

- Fixed release date for version 3. [Jose Diaz-Gonzalez]

3 (2012-11-25)
--------------

- Added requirements files to manifest. [Jose Diaz-Gonzalez]

- Include all contrib files in release. [Jose Diaz-Gonzalez]

- Revert "removed redundant README.txt" to follow pypi standards. [Jose
  Diaz-Gonzalez]

  This reverts commit e667f63706e0af8bc82c0eac6eac43318144e107.

- Added bash startup script. Closes #35. [Jose Diaz-Gonzalez]

- Added an example supervisor config for redis. closes #34. [Jose Diaz-
  Gonzalez]

- Removed redundant README.txt. [Jose Diaz-Gonzalez]

- Added classifiers to package. [Jose Diaz-Gonzalez]

- Re-order workers. [Jose Diaz-Gonzalez]

- Re-require pika. [Jose Diaz-Gonzalez]

- Make zeromq installation optional. [Morgan Delagrange]

- Formatting. [Jose Diaz-Gonzalez]

- Added changes to changelog for version 3. [Jose Diaz-Gonzalez]

- Timestamp in ISO 8601 format with the "Z" sufix to express UTC.
  [Xabier de Zuazo]

- Adding udp support. [Morgan Delagrange]

- Lpush changed to rpush on redis transport. This is required to always
  read the events in the correct order on the logstash side. See: https:
  //github.com/logstash/logstash/blob/6f745110671b5d9d66bf082fbfed99d145
  af4620/lib/logstash/outputs/redis.rb#L4. [Xabier de Zuazo]

2 (2012-10-25)
--------------

- Example upstart script. [Michael D'Auria]

- Fixed a few more import statements. [Jose Diaz-Gonzalez]

- Fixed binary call. [Jose Diaz-Gonzalez]

- Refactored logging. [Jose Diaz-Gonzalez]

- Improve logging. [Michael D'Auria]

- Removed unnecessary print statements. [Jose Diaz-Gonzalez]

- Add default stream handler when transport is stdout. Closes #26. [bear
  (Mike Taylor)]

- Handle the case where the config file is not present. [Michael
  D'Auria]

- Better exception handling for unhandled exceptions. [Michael D'Auria]

- Fix wrong addfield values. [Alexander Fortin]

- Add add_field to config example. [Alexander Fortin]

- Add support for add_field into config file. [Alexander Fortin]

- Minor readme updates. [Jose Diaz-Gonzalez]

- Add support for type reading from INI config file. [Alexander Fortin]

  Add support for symlinks in config file
  
  Add support for file globbing in config file
  
  Add support for tags
  
  
  a little bit of refactoring, move type and tags check down into
  transport class
  
  create config object (reading /dev/null) even if no config file
  has been given via cli
  
  Add documentation for INI file to readme
  
  Remove unused json library
  
  Conflicts:
  README.rst

- When sending data over the wire, use UTC timestamps. [Darren Worrall]

- Support globs in file paths. [Darren Worrall]

- Added msgpack support. [Jose Diaz-Gonzalez]

- Use the python logging framework. [Jose Diaz-Gonzalez]

- Fixed Transport.format() method. [Jose Diaz-Gonzalez]

- Properly parse BEAVER_FILES env var. [Jose Diaz-Gonzalez]

- Refactor transports. [Jose Diaz-Gonzalez]

  Fix the json import to use the fastest json module available
  
  Move formatting into Transport class

- Attempt to fix defaults from env variables. [Jose Diaz-Gonzalez]

- Fix README and beaver CLI help to reference correct RABBITMQ_HOST
  environment variable. [jdutton]

- Add RabbitMQ support. [Alexander Fortin]

- Added real-world example of beaver usage for tailing a file. [Jose
  Diaz-Gonzalez]

- Removed unused argument. [Jose Diaz-Gonzalez]

- Ensure that python-compatible readme is included in package. [Jose
  Diaz-Gonzalez]

- Fix variable naming and timeout for redis transport. [Jose Diaz-
  Gonzalez]

- Installation instructions. [Jose Diaz-Gonzalez]

- Use restructured text for readme instead of markdown. [Jose Diaz-
  Gonzalez]

- Removed unnecessary .gitignore. [Jose Diaz-Gonzalez]

1 (2012-08-06)
--------------

- Moved app into python package format. [Jose Diaz-Gonzalez]

- Moved binary beaver.py to bin/beaver, as per python packaging. [Jose
  Diaz-Gonzalez]

- Moved around transports to be independent of each other. [Jose Diaz-
  Gonzalez]

- Reorder transports. [Jose Diaz-Gonzalez]

- Rewrote run_worker to throw exception if all transport options have
  been exhausted. [Jose Diaz-Gonzalez]

- Rename Amqp -> Zmq to avoid confusion with RabbitMQ. [Alexander
  Fortin]

- Added choices to the --transport argument. [Jose Diaz-Gonzalez]

- Fixed derpy formatting. [Jose Diaz-Gonzalez]

- Added usage to the readme. [Jose Diaz-Gonzalez]

- Support usage of environment variables instead of arguments. [Jose
  Diaz-Gonzalez]

- Fixed files argument parsing. [Jose Diaz-Gonzalez]

- One does not simply license all the things. [Jose Diaz-Gonzalez]

- Add todo to readme. [Jose Diaz-Gonzalez]

- Added version to pyzmq. [Jose Diaz-Gonzalez]

- Added license. [Jose Diaz-Gonzalez]

- Reordered imports. [Jose Diaz-Gonzalez]

- Moved all transports to beaver/transports.py. [Jose Diaz-Gonzalez]

- Calculate current timestamp at most once per callback fired. [Jose
  Diaz-Gonzalez]

- Modified transports to include proper information for ingestion in
  logstash. [Jose Diaz-Gonzalez]

- Fixed package imports. [Jose Diaz-Gonzalez]

- Removed another compiled python file. [Jose Diaz-Gonzalez]

- Use ujson instead of simplejson. [Jose Diaz-Gonzalez]

- Ignore compiled python files. [Jose Diaz-Gonzalez]

- Fixed imports. [Jose Diaz-Gonzalez]

- Fixed up readme instructions. [Jose Diaz-Gonzalez]

- Refactor transports so that connections are no longer global. [Jose
  Diaz-Gonzalez]

- Readme and License. [Jose Diaz-Gonzalez]

