# MacOS Sierra 에서 MySQL2 설치 시 오류 해결

> Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries.
Generally there are no consequences of this for you. If you build your own software and it requires this formula, you'll need to add to your build variables:
LDFLAGS: -L/usr/local/opt/openssl/lib
CPPFLAGS: -I/usr/local/opt/openssl/include
PKG_CONFIG_PATH: /usr/local/opt/openssl/lib/pkgconfig

```bash
bundle config --local build.mysql2 "--with-ldflags=-L/usr/local/opt/openssl/lib --with-cppflags=-I/usr/local/opt/openssl/include"
```

#### 출처

[Stack Overflow "Can't install mysql2 gem on macOS Sierra"](http://stackoverflow.com/questions/39617761/cant-install-mysql2-gem-on-macos-sierra)