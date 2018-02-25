
# amdevtok - Apple Music Developer Token creation utility based on JWT C Library
A simple command line program amdevtok to generate Apple Music Developer Token. Based on JWT C Library by Ben Collins.

## Build Requirements

- https://github.com/akheron/jansson
- OpenSSL or GnuTLS

## Documentation

[GitHub Pages](http://benmcollins.github.io/libjwt/)

[Apple Music Developer Token](https://developer.apple.com/library/content/documentation/NetworkingInternetWeb/Conceptual/AppleMusicWebServicesReference/SetUpWebServices.html)

## Prerequisite

- cmake
- autoconf
- autoreconf
- automake
- libtool
- jansson
- jansson-devel
- openssl
- openssl-devel
- check
- check-devel
- patch

## Build Instructions

1. Apply amdevtok patch
- patch -p1 < ./amdevtok.diff

2. Compile libjwt
- 2.1 **With GNU Make:** Use ``autoreconf -i`` to create project files 
- 2.2 ``./configure``.
- 2.3 ``make all``: build library.

Because amdevtok add non-standard function to the original libjwt source, it is staticly linked to libjwt object
files, so there is no need to make install to install libjwt libraries into system.

3. Compile amdevtok
- ``sh make-amdevtok``

This will compile amdevtok binary and create a symbol link amdevtokd, please note the trailing 'd'.<br>
amdevtok will just print result, amdevtokd will also print the original payload.

## How to use amdevtok
amdevtok is static linked and can be copied anywhere has openssl/GnuTLS and jansson support. Usage is very straightfoward.<br>
1. Have your private key(.p8 file), kid and team id ready; 
2. execute amdevtok; 
3. Copy the results and go.<br>
<br>
Usage: amdevtok private_key kid teamid [exp-length-in-seconds]<br>
<br>
By default, expiration is plus 90 days:<br>
&nbsp;&nbsp;./amdevtok /path/to/my.p8 ABC123DEFG DEF123GHIJ<br>
<br>
Add 4th optional parameter to specify expiration period, eg. Expire in 1 hour:<br>
&nbsp;&nbsp;./amdevtok /path/to/my.p8 ABC123DEFG DEF123GHIJ 3600<br>
<br>
To print payload:<br>
&nbsp;&nbsp;./amdevtok<B>d</B> /path/to/my.p8 ABC123DEFG DEF123GHIJ<br>
<br>
Example output:<br>
#./amdevtok<B>d</B> ./AuthKey_ABC123DEFG.p8 ABC123DEFG DEF123GHIJ<br>
{<br>
&nbsp;&nbsp;&nbsp;&nbsp;"alg": "ES256",<br>
&nbsp;&nbsp;&nbsp;&nbsp;"kid": "ABC123DEFG"<br>
}<br>
<br>
{<br>
&nbsp;&nbsp;&nbsp;&nbsp;"exp": 1527368388,<br>
&nbsp;&nbsp;&nbsp;&nbsp;"iat": 1519592388,<br>
&nbsp;&nbsp;&nbsp;&nbsp;"iss": "DEF123GHIJ"<br>
}<br>
ewogICAgImFsasdfasdfasdfCAia2lkIjogasdfasdfiCn0K.CnsKICAgICJleHAiOasdfasdfasdfImlhdCI6IDE1MTfasdfasdfXNzIjogIkRFRjEyasdfaISUoiCn0K.61234124asdfffCU0KWgc0vmOPgENzb3sasdfasdfnfasdfzCl1IohAA<br>
