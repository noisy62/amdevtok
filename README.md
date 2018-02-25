![LibJWT Logo](https://user-images.githubusercontent.com/320303/33439880-82406da4-d5bc-11e7-8959-6d53553c1984.png)

# amdevtok - Apple Music Developer Token creation utility based on JWT C Library

[![Build Status](https://travis-ci.org/benmcollins/libjwt.svg?branch=master)](https://travis-ci.org/benmcollins/libjwt) [![codecov.io](http://codecov.io/github/benmcollins/libjwt/coverage.svg?branch=master)](http://codecov.io/github/benmcollins/libjwt?branch=master)

[![View on JWT.IO](https://jwt.io/assets/badge.svg)](https://jwt.io)

## Build Requirements

- https://github.com/akheron/jansson
- OpenSSL or GnuTLS

## Documentation

[GitHub Pages](http://benmcollins.github.io/libjwt/)

## Pre-built Ubuntu Packages (PPA)

`sudo add-apt-repository ppa:ben-collins/libjwt`

## Build Instructions

## Apply amdevtok patch
- patch -p1 < ./amdevtok.diff

**With GNU Make:** Use ``autoreconf -i`` to create project files and run ``./configure``.
- ``make all``: build library.
- ``make check``: build and run test suite.
- See INSTALL file for more details on GNU Auto tools and GNU Make.
- Use the ``--without-openssl`` with ``./configure`` to use GnuTLS.

## Compile amdevtok
- sh make-amdevtok
This will compile amdevtok binary and create a symbol link amdevtokd, please note the trailing 'd'.
amdevtok will just print result, amdevtokd will also print the original payload.

## Use amdevtok
Have your private key, kid and team id ready, execute amdevtok. Command line sytax:

  amdevtok private_key kid teamid [exp-length-in-seconds]

By default, expiration is plus 90 days:
  ./amdevtok /path/to/my.p8 ABC123DEFG DEF123GHIJ

Add 4th optional parameter to specify expiration period, eg. Expire in 1 hour:
    ./amdevtok /path/to/my.p8 ABC123DEFG DEF123GHIJ 3600
    
To print payload:
    ./amdevtokd /path/to/my.p8 ABC123DEFG DEF123GHIJ

Example:
#./amdevtokd ./AuthKey_ABC123DEFG.p8 ABC123DEFG DEF123GHIJ
{
    "alg": "ES256",
    "kid": "ABC123DEFG"
}

{
    "exp": 1527368388,
    "iat": 1519592388,
    "iss": "DEF123GHIJ"
}
ewogICAgImFsasdfasdfasdfCAia2lkIjogasdfasdfiCn0K.CnsKICAgICJleHAiOasdfasdfasdfImlhdCI6IDE1MTfasdfasdfXNzIjogIkRFRjEyasdfaISUoiCn0K.61234124asdfffCU0KWgc0vmOPgENzb3sasdfasdfnfasdfzCl1IohAA
