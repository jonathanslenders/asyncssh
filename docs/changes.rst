.. currentmodule:: asyncssh

Change Log
==========

Release 1.2.0 (6 Jun 2015)
--------------------------

* Fixed a problem with the SSHConnection context manager on Python versions
  older than 3.4.2.

* Updated the documentation for get_extra_info() in the SSHConnection,
  SSHChannel, SSHReader, and SSHWriter classes to contain pointers
  to get_extra_info() in their parent transports to make it easier to
  see all of the attributes which can be queried.

* Clarified the legal return values for the session_requested(),
  connection_requested(), and server_requested() methods in
  SSHServer.

* Eliminated calls to the deprecated importlib.find_loader() method.

* Made improvements to README suggested by Nicholas Chammas.

* Fixed a number of issues identified by pylint.

Release 1.1.1 (25 May 2015)
---------------------------

* Added new start_sftp_server method on SSHChannel to allow applications
  using the non-streams API to start an SFTP server.

* Enhanced the default format_longname() method in SFTPServer to properly
  handle the case where not all of the file attributes are returned by
  stat().

* Fixed a bug related to the new allow_pty parameter in create_server.

* Fixed a bug in the hashed known_hosts support introduced in some recent
  refactoring of the host pattern matching code.

Release 1.1.0 (22 May 2015)
---------------------------

* SFTP is now supported!

  * Both client and server support is available.
  * SFTP version 3 is supported, with OpenSSH extensions.
  * Recursive transfers and glob matching are supported in the client.
  * File I/O APIs allow files to be accessed without downloading them.

* New simplified connect and listen APIs have been added.

* SSHConnection can now be used as a context manager.

* New arguments to create_server now allow the specification of a
  session_factory and encoding or sftp_factory as well as controls
  over whether a pty is allowed and the window and max packet size,
  avoiding the need to create custom SSHServer subclasses or custom
  SSHServerChannel instances.

* New examples have been added for SFTP and to show the use of the new
  connect and listen APIs.

* Copyrights in changed files have all been updated to 2015.

Release 1.0.1 (13 Apr 2015)
---------------------------

* Fixed a bug in OpenSSH private key encryption introduced in some
  recent cipher refactoring.

* Added bcrypt and libnacl as optional dependencies in setup.py.

* Changed test_keys test to work properly when bcrypt or libnacl aren't
  installed.

Release 1.0.0 (11 Apr 2015)
---------------------------

* This release finishes adding a number of major features, finally making
  it worthy of being called a "1.0" release.

* Host and user certificates are now supported!

  * Enforcement is done on principals in certificates.
  * Enforcement is done on force-command and source-address critical options.
  * Enforcement is done on permit-pty and permit-port-forwarding extensions.

* OpenSSH-style known hosts files are now supported!

  * Positive and negative wildcard and CIDR-style patterns are supported.
  * HMAC-SHA1 hashed host entries are supported.
  * The @cert-authority and @revoked markers are supported.

* OpenSSH-style authorized keys files are now supported!

  * Both client keys and certificate authorities are supported.
  * Enforcement is done on from and principals options during key matching.
  * Enforcement is done on no-pty, no-port-forwarding, and permitopen.
  * The command and environment options are supported.
  * Applications can query for their own non-standard options.

* Support has been added for OpenSSH format private keys.

  * DSA, RSA, and ECDSA keys in this format are now supported.
  * Ed25519 keys are supported when libnacl and libsodium are installed.
  * OpenSSH private key encryption is supported when bcrypt is installed.

* Curve25519 Diffie-Hellman key exchange is now available via either the
  curve25519-donna or libnacl and libsodium packages.

* ECDSA key support has been enhanced.

  * Support is now available for PKCS#8 ECDSA v2 keys.
  * Support is now available for both NamedCurve and explicit ECParameter
    versions of keys, as long as the parameters match one of the supported
    curves (nistp256, nistp384, or nistp521).

* Support is now available for the OpenSSH chacha20-poly1305 cipher when
  libnacl and libsodium are installed.

* Cipher names specified in private key encryption have been changed to be
  consistent with OpenSSH cipher naming, and all SSH ciphers can now be
  used for encryption of keys in OpenSSH private key format.

* A couple of race conditions in SSHChannel have been fixed and channel
  cleanup is now delayed to allow outstanding message handling to finish.

* Channel exceptions are now properly delivered in the streams API.

* A bug in SSHStream read() where it could sometimes return more data than
  requested has been fixed. Also, read() has been changed to properly block
  and return all data until EOF or a signal is received when it is called
  with no length.

* A bug in the default implementation of keyboard-interactive authentication
  has been fixed, and the matching of a password prompt has been loosened
  to allow it to be used for password authentication on more devices.

* Missing code to resume reading after a stream is paused has been added.

* Improvements have been made in the handling of canceled requests.

* The test code has been updated to test Ed25519 and OpenSSH format
  private keys.

* Examples have been updated to reflect some of the new capabilities.

Release 0.9.2 (26 Jan 2015)
---------------------------

* Fixed a bug in PyCrypto CipherFactory introduced during PyCA refactoring.

Release 0.9.1 (3 Dec 2014)
--------------------------

* Added some missing items in setup.py and MANIFEST.in.

* Fixed the install to work even when cryptographic dependencies aren't
  yet installed.

* Fixed an issue where get_extra_info calls could fail if called when
  a connection or session was shutting down.

Release 0.9.0 (14 Nov 2014)
---------------------------

* Added support to use PyCA (0.6.1 or later) for cryptography. AsyncSSH
  will automatically detect and use either PyCA, PyCrypto, or both depending
  on which is installed and which algorithms are requested.

* Added support for AES-GCM ciphers when PyCA is installed.

Release 0.8.4 (12 Sep 2014)
---------------------------

* Fixed an error in the encode/decode functions for PKCS#1 DSA public keys.

* Fixed a bug in the unit test code for import/export of RFC4716 public keys.

Release 0.8.3 (16 Aug 2014)
---------------------------

* Added a missing import in the curve25519 implementation.

Release 0.8.2 (16 Aug 2014)
---------------------------

* Provided a better long description for PyPI.

* Added link to PyPI in documentation sidebar.

Release 0.8.1 (15 Aug 2014)
---------------------------

* Added a note in the :meth:`validate_public_key()
  <SSHServer.validate_public_key>` documentation clarifying that AsyncSSH
  will verify that the client possesses the corresponding private key before
  authentication is allowed to succeed.

* Switched from setuptools to distutils and added an initial set of unit
  tests.

* Prepared the package to be uploaded to PyPI.

Release 0.8.0 (15 Jul 2014)
---------------------------

* Added support for Curve25519 Diffie Hellman key exchange on systems with
  the curve25519-donna Python package installed.

* Updated the examples to more clearly show what values are returned even
  when not all of the return values are used.

Release 0.7.0 (7 Jun 2014)
--------------------------

* This release adds support for the "high-level" ``asyncio`` streams API,
  in the form of the :class:`SSHReader` and :class:`SSHWriter` classes
  and wrapper methods such as :meth:`open_session()
  <SSHClientConnection.open_session>`, :meth:`open_connection()
  <SSHClientConnection.open_connection>`, and :meth:`start_server()
  <SSHClientConnection.start_server>`. It also allows the callback
  methods on :class:`SSHServer` to return either SSH session objects or
  handler functions that take :class:`SSHReader` and :class:`SSHWriter`
  objects as arguments. See :meth:`session_requested()
  <SSHServer.session_requested>`, :meth:`connection_requested()
  <SSHServer.connection_requested>`, and :meth:`server_requested()
  <SSHServer.server_requested>` for more information.

* Added new exceptions :exc:`BreakReceived`, :exc:`SignalReceived`, and
  :exc:`TerminalSizeChanged` to report when these messages are received
  while trying to read from an :class:`SSHServerChannel` using the new
  streams API.

* Changed :meth:`create_server() <SSHClientConnection.create_server>` to
  accept either a callable or a coroutine for its ``session_factory``
  argument, to allow asynchronous operations to be used when deciding
  whether to accept a forwarded TCP connection.

* Renamed ``accept_connection()`` to :meth:`create_connection()
  <SSHServerConnection.create_connection>` in the :class:`SSHServerConnection`
  class for consistency with :class:`SSHClientConnection`, and added a
  corresponding :meth:`open_connection() <SSHServerConnection.open_connection>`
  method as part of the streams API.

* Added :meth:`get_exit_status() <SSHClientChannel.get_exit_status>` and
  :meth:`get_exit_signal() <SSHClientChannel.get_exit_signal>` methods
  to the :class:`SSHClientChannel` class.

* Added :meth:`get_command() <SSHServerChannel.get_command>` and
  :meth:`get_subsystem() <SSHServerChannel.get_subsystem>` methods to
  the :class:`SSHServerChannel` class.

* Fixed the name of the :meth:`write_stderr() <SSHServerChannel.write_stderr>`
  method and added the missing :meth:`writelines_stderr()
  <SSHServerChannel.writelines_stderr>` method to the :class:`SSHServerChannel`
  class for outputting data to the stderr channel.

* Added support for a return value in the :meth:`eof_received()
  <SSHClientSession.eof_received>` of :class:`SSHClientSession`,
  :class:`SSHServerSession`, and :class:`SSHTCPSession` to support
  half-open channels. By default, the channel is automatically closed
  after :meth:`eof_received() <SSHClientSession.eof_received>` returns,
  but returning ``True`` will now keep the channel open, allowing output
  to still be sent on the half-open channel. This is done automatically
  when the new streams API is used.

* Added values ``'local_peername'`` and ``'remote_peername'`` to the set
  of information available from the :meth:`get_extra_info()
  <SSHTCPChannel.get_extra_info>` method in the :class:`SSHTCPChannel` class.

* Updated functions returning :exc:`IOError` or :exc:`socket.error` to
  return the new :exc:`OSError` exception introduced in Python 3.3.

* Cleaned up some errors in the documentation.

* The :ref:`API`, :ref:`ClientExamples`, and :ref:`ServerExamples` have
  all been updated to reflect these changes, and new examples showing the
  streams API have been added.

Release 0.6.0 (11 May 2014)
---------------------------

* This release is a major revamp of the code to migrate from the
  ``asyncore`` framework to the new ``asyncio`` framework in Python
  3.4. All the APIs have been adapted to fit the new ``asyncio``
  paradigm, using coroutines wherever possible to avoid the need
  for callbacks when performing asynchronous operations.

  So far, this release only supports the "low-level" ``asyncio`` API.

* The :ref:`API`, :ref:`ClientExamples`, and :ref:`ServerExamples` have
  all been updated to reflect these changes.


Release 0.5.0 (11 Oct 2013)
---------------------------

* Added the following new classes to support fully asynchronous
  connection forwarding, replacing the methods previously added in
  release 0.2.0:

  * :class:`SSHClientListener`
  * :class:`SSHServerListener`
  * :class:`SSHClientLocalPortForwarder`
  * :class:`SSHClientRemotePortForwarder`
  * :class:`SSHServerPortForwarder`

  These new classes allow for DNS lookups and other operations to be
  performed fully asynchronously when new listeners are set up. As with
  the asynchronous connect changes below, methods are now available
  to report when the listener is opened or when an error occurs during
  the open rather than requiring the listener to be fully set up in a
  single call.

* Updated examples in :ref:`ClientExamples` and :ref:`ServerExamples`
  to reflect the above changes.

Release 0.4.0 (28 Sep 2013)
---------------------------

* Added support in :class:`SSHTCPConnection` for the following methods
  to allow asynchronous operations to be used when accepting inbound
  connection requests:

  * :meth:`handle_open_request() <SSHTCPConnection.handle_open_request>`
  * :meth:`report_open() <SSHTCPConnection.report_open>`
  * :meth:`report_open_error() <SSHTCPConnection.report_open_error>`

  These new methods are used to implement asynchronous connect
  support for local and remote port forwarding, and to support
  trying multiple destination addresses when connection failures
  occur.

* Cleaned up a few minor documentation errors.

Release 0.3.0 (26 Sep 2013)
---------------------------

* Added support in :class:`SSHClient` and :class:`SSHServer` for setting
  the key exchange, encryption, MAC, and compression algorithms allowed
  in the SSH handshake.

* Refactored the algorithm selection code to pull a common matching
  function back into ``_SSHConnection`` and simplify other modules.

* Extended the listener class to open multiple listening sockets when
  necessary, fixing a bug where sockets opened to listen on ``localhost``
  were not properly accepting both IPv4 and IPv6 connections.

  Now, any listen request which resolves to multiple addresses will open
  listening sockets for each address.

* Fixed a bug related to tracking of listeners opened on dynamic ports.

Release 0.2.0 (21 Sep 2013)
---------------------------

* Added support in :class:`SSHClient` for the following methods related
  to performing standard SSH port forwarding:

  * :meth:`forward_local_port() <SSHClient.forward_local_port>`
  * :meth:`cancel_local_port_forwarding() <SSHClient.cancel_local_port_forwarding>`
  * :meth:`forward_remote_port() <SSHClient.forward_remote_port>`
  * :meth:`cancel_remote_port_forwarding() <SSHClient.cancel_remote_port_forwarding>`
  * :meth:`handle_remote_port_forwarding() <SSHClient.handle_remote_port_forwarding>`
  * :meth:`handle_remote_port_forwarding_error() <SSHClient.handle_remote_port_forwarding_error>`

* Added support in :class:`SSHServer` for new return values in
  :meth:`handle_direct_connection() <SSHServer.handle_direct_connection>`
  and :meth:`handle_listen() <SSHServer.handle_listen>` to activate
  standard SSH server-side port forwarding.

* Added a client_addr argument and member variable to :class:`SSHServer`
  to hold the client's address information.

* Added and updated examples related to port forwarding and using
  :class:`SSHTCPConnection` to open direct and forwarded TCP
  connections in :ref:`ClientExamples` and :ref:`ServerExamples`.

* Cleaned up some of the other documentation.

* Removed a debug print statement accidentally left in related to
  SSH rekeying.

Release 0.1.0 (14 Sep 2013)
---------------------------

* Initial release
