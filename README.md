Nagios plugin to check amavisd-new daemon
=========================================

`check_amavis` checks if [amavisd-new][1] daemon is working and if its antivirus engine is working.

This check talks with amavisd-new daemon (default port is 10024) with SMTP protocol.
It tests if the daemon is up and if it's able to scan an email with a virus (EICAR test virus is sent).

Please note that if `amavisd-new` is run on a different machine, you should enable the connection from nagios ip address (take a look at `amavisd.conf`).

This Perl script needs [GetOpt::Long][2], [MIME::Tools][3] and [Net::SMTP][4] to work.

Parameters:

 - `--server` amavisd-new address (mandatory)
 - `--port` amavisd-new port (default 10024)
 - `--from` sender email address (mandatory)
 - `--to` recipient address (if not present copied from `--from`)
 - `--debug` useful for debugging (launch it at command line)

Command configuration: 
```
define command {
    command_name check_amavis 
    command_line $USER1$/check_amavis.pl --server $HOSTADDRESS$ --from email_address --to email_address --port 10024 
}
```

where `email_address` is a valid email address handled by amavisd.

## Copyright

License: GPL v2

(c) 2011-2014 Elan Ruusamäe <glen@pld-linux.org> (maintainer from version 1.1 and upwards)

  [1]: http://www.amavis.org/
  [2]: http://perldoc.perl.org/Getopt/Long.html
  [3]: http://search.cpan.org/perldoc?MIME::Tools
  [4]: http://search.cpan.org/perldoc?Net::SMTP
