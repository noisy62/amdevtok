![LibJWT Logo](https://user-images.githubusercontent.com/320303/33439880-82406da4-d5bc-11e7-8959-6d53553c1984.png)

# amdevtok - Apple Music Developer Token creation utility based on JWT C Library

[![Build Status](https://travis-ci.org/benmcollins/libjwt.svg?branch=master)](https://travis-ci.org/benmcollins/libjwt) [![codecov.io](http://codecov.io/github/benmcollins/libjwt/coverage.svg?branch=master)](http://codecov.io/github/benmcollins/libjwt?branch=master)

[![View on JWT.IO](https://jwt.io/assets/badge.svg)](https://jwt.io)

## Build Requirements

- https://github.com/akheron/jansson
- OpenSSL or GnuTLS

## Documentation

[GitHub Pages](http://benmcollins.github.io/libjwt/)

[Apple Music Developer Token](https://developer.apple.com/library/content/documentation/NetworkingInternetWeb/Conceptual/AppleMusicWebServicesReference/SetUpWebServices.html)

## Pre-built Ubuntu Packages (PPA)

`sudo add-apt-repository ppa:ben-collins/libjwt`

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
- sh make-amdevtok
This will compile amdevtok binary and create a symbol link amdevtokd, please note the trailing 'd'.
amdevtok will just print result, amdevtokd will also print the original payload.

## How to use amdevtok
amdevtok is static linked and can be copied anywhere has openssl/GnuTLS support. Usage is very straight foward. 
Have your private key(.p8 file), kid and team id ready, execute amdevtok. Copy the results and go.

- Command line sytax:

  amdevtok private_key kid teamid [exp-length-in-seconds]

- By default, expiration is plus 90 days:
  ./amdevtok /path/to/my.p8 ABC123DEFG DEF123GHIJ

- Add 4th optional parameter to specify expiration period, eg. Expire in 1 hour:
    ./amdevtok /path/to/my.p8 ABC123DEFG DEF123GHIJ 3600
    
- To print payload:
    ./amdevtokd /path/to/my.p8 ABC123DEFG DEF123GHIJ

- Example output:<br>
#./amdevtokd ./AuthKey_ABC123DEFG.p8 ABC123DEFG DEF123GHIJ<br>
{<br>
    "alg": "ES256",<br>
    "kid": "ABC123DEFG"<br>
}<br>
<br>
{<br>
    "exp": 1527368388,<br>
    "iat": 1519592388,<br>
    "iss": "DEF123GHIJ"<br>
}<br>
ewogICAgImFsasdfasdfasdfCAia2lkIjogasdfasdfiCn0K.CnsKICAgICJleHAiOasdfasdfasdfImlhdCI6IDE1MTfasdfasdfXNzIjogIkRFRjEyasdfaISUoiCn0K.61234124asdfffCU0KWgc0vmOPgENzb3sasdfasdfnfasdfzCl1IohAA<br>
