.. include:: /Includes.txt
.. highlight:: shell
.. index:: pair:DDEV; Troubleshooting
.. _DDEV-Troubleshooting:

====================
DDEV Troubleshooting
====================


Port is already in use
======================

Using PHP to test
-----------------

Try to run the builtin server of PHP and see if it runs. Press :kkb:`Ctrl+C`
to stop the server.

Example: Find that port 80 is already in use::

   ➜  php -S localhost:80
   [Fri Feb  5 10:51:08 2021] Failed to listen on localhost:80 (reason: Permission denied)

   ➜  # Server did not start.
   ➜  # This means: Port 80 is already in use and thus not free.


Example: Find that port 4430 is free for use::

   ➜  php -S localhost:4430
   [Fri Feb  5 11:01:58 2021] PHP 8.0.1 Development Server (http://localhost:4430) started
   ^C%                                                                                                                     ➜  ~

   ➜  # Server did start.
   ➜  # This means: Port 4430 is not used otherwise and free for use.


Using Python to test
--------------------

Try to run the builtin server of Python and see if it runs. Press :kbd:`Ctrl+C`
to stop the server. Examples:

Example: Find that port 80 is already in use::

   ➜  python3 -m http.server 80
   Traceback (most recent call last):
     File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
       return _run_code(code, main_globals, None,
     File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
       exec(code, run_globals)
     File "/usr/lib/python3.8/http/server.py", line 1294, in <module>
       test(
     File "/usr/lib/python3.8/http/server.py", line 1249, in test
       with ServerClass(addr, HandlerClass) as httpd:
     File "/usr/lib/python3.8/socketserver.py", line 452, in __init__
       self.server_bind()
     File "/usr/lib/python3.8/http/server.py", line 1292, in server_bind
       return super().server_bind()
     File "/usr/lib/python3.8/http/server.py", line 138, in server_bind
       socketserver.TCPServer.server_bind(self)
     File "/usr/lib/python3.8/socketserver.py", line 466, in server_bind
       self.socket.bind(self.server_address)
   PermissionError: [Errno 13] Permission denied

   ➜  # Server did not start.
   ➜  # This means: Port 80 is already in use and thus not free.


Example: Find that port 4430 is free for use::

   ➜  python3 -m http.server 4430
   Serving HTTP on 0.0.0.0 port 4430 (http://0.0.0.0:4430/) ...
   ^C
   Keyboard interrupt received, exiting.

   ➜  # Server did start.
   ➜  # This means: Port 4430 is not used otherwise and free for use.
