# LinOTP-and-FreeRadius
LinOtp and FreeRadius on Centos 7

Install freeradius:

yum install freeradius
yum install freeradius-perl
yum install freeradius-utils

Install Perl modules:
yum install perl-Try-Tiny
yum install perl-LWP-Protocol-https

Copy:
rm /etc/raddb/{clients.conf,users}
cp linotp /etc/raddb/sites-available/linotp
cp perl /etc/raddb/mods-available/perl
cp users /etc/raddb/users
cp clients.conf /etc/raddb/clients.conf
cp radius_linotp.pm /usr/lib/linotp/radius_linotp.pm

Link:
rm /etc/raddb/sites-enabled/{default,inner-tunnel,}
rm /etc/raddb/mods-enabled/eap
cd /etc/raddb/sites-enabled/
ln -s ../sites-available/linotp /etc/raddb/sites-enabled
cd /etc/raddb/mods-enabled
ln -s ../mods-available/perl /etc/raddb/mods-enabled


I am not using ini file for configuring LinOTP server, instead config parameters are defined directly in .pm file  
Edit this part of radius_linotp.pm to your environment specifications:

    $Config->{URL}       = 'https://_linotpserver.example.com_/validate/simplecheck';
    $Config->{REALM}     = 'example.com';
