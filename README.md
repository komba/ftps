FTPS
=============

FTPS extends the core Net::FTP class to provide implicit and explicit FTPS support.

Install
-------

    $ [sudo] gem install ftps

**Note**: Your Ruby installation must have OpenSSL support.

Usage
-----
    require 'ftps'

Example 1:

    # Connect to a host using explicit FTPS and do not verify the host's cert
    ftps = FTPS.new
    ftps.ssl_context = FTPS.create_ssl_context(:verify_mode => OpenSSL::SSL::VERIFY_NONE)
    ftps.connect('some host')
    ftps.login('usr', 'passwd')

Example 2:

    FTPS.open('host', 'usr', 'passwd', nil, FTPS::IMPLICIT) do |ftps|
      ...
    end

Interface
---------

    # Constants used for setting FTPS mode
    FTPS::EXPLICIT
    FTPS::IMPLICIT

    FTPS.new(host = nil, user = nil, passwd = nil, acct = nil, ftps_mode = EXPLICIT, ssl_context_params = {})
    FTPS.open(host, user = nil, passwd = nil, acct = nil, ftps_mode = EXPLICIT, ssl_context_params = {})

    # Returns an OpenSSL::SSL::SSLContext using params to set set the corresponding SSLContext attributes.
    FTPS.create_ssl_context(params = {})

    # Set the FTPS mode to implicit (FTPS::IMPLICIT) or explicit (FTPS::EXPLICIT).
    # The default FTPS mode is explicit.
    ftps_mode=(ftps_mode)

    # Same as Net::FTP.connect, but will use port 990 when using implicit FTPS and a port is not specified.
    connect(host, port = ftps_implicit? ? IMPLICIT_PORT : FTP_PORT)

    # Same as Net::FTP.login, but with optional auth param to control the value that is sent with the AUTH command.
    login(user = 'anonymous', passwd = nil, acct = nil, auth = 'TLS')

    ftps_explicit?
    ftps_implicit?

More Information
----------------

* [Net::FTP RDoc](http://ruby-doc.org/stdlib/libdoc/net/ftp/rdoc/index.html)
* [OpenSSL RDoc](http://ruby-doc.org/stdlib/libdoc/openssl/rdoc/index.html)

License
-------
Copyright © 2011, Bryan Nix. FTPS is released under the MIT license. See LICENSE file for details.
