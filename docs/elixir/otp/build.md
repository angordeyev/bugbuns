# Build

We will use the latest Debian image.

```shell
docker run -it --name build-erlang debian
```

## Prerequisites

```shell
apt-get update &&
apt-get install -y git curl build-essential automake autoconf libssl-dev libncurses5-dev &&

mkdir /src && cd $_
```

## Using make

Get OTP sources:

```shell
git clone https://github.com/erlang/otp.git
cd otp
```

Build:

```shell
./configure
make
make install
```

## Using kerl

```shell
curl -O https://raw.githubusercontent.com/kerl/kerl/master/kerl &&
chmod a+x kerl &&

./kerl build 27.0-rc1 27.0-rc1.
```


Install and activate:

```shell
./kerl list builds
```

```shell
./kerl install 27.0-rc1. /usr/local/lib/erlang/27.0-rc1.
```

```shell
. /usr/local/lib/erlang/27.0-rc1./activate
```

## All in One

```shell
docker run -it debian
```

```shell
apt-get update &&
apt-get install -y git curl build-essential automake autoconf libssl-dev libncurses5-dev

mkdir /src &&
cd $_ &&

git clone https://github.com/erlang/otp.git
cd otp

./configure
make
make install
```

## Bootstrap

```shell
apt-get update &&
apt-get install -y git curl build-essential automake autoconf libssl-dev libncurses5-dev

mkdir /src &&
cd $_ &&

git clone https://github.com/erlang/otp.git
cd otp

./configure --enable-bootstrap-only
make
make install
```

## KERL Minimal Configuration Options

```shell
export KERL_CONFIGURE_OPTIONS="--disable-debug \
--disable-silent-rules \
--disable-dynamic-ssl-lib \
--disable-hipe \
--disable-kernel-poll \
--disable-sctp \
--disable-shared-zlib \
--disable-smp-support \
--disable-threads \
--disable-wx \
--without-ssl \
--without-jinterface \
--without-odbc \
--without-wx"
```

```shell
export KERL_CONFIGURE_OPTIONS="--without-ssl \
--disable-hipe \
--disable-smp-support \
--without-jinterface \
--without-odbc \
--without-wx"
```

```shell
./kerl build 27.0-rc1 27.0-rc1.
```

https://www.erlang.org/doc/installation_guide/install#Advanced-configuration-and-build-of-ErlangOTP_Configuring

## GRISP Compilation

https://github.com/grisp/grisp/blob/master/grisp/grisp2/common/build/files/xcomp/erl-xcomp-arm-rtems5.conf

## Resources

* [ERTS Docs. Erlang Repo.](https://github.com/erlang/otp/blob/master/erts/doc/references/erlc_cmd.md)
* [Unify builds for otp/erts/* targets? Erlang Forums.](https://erlangforums.com/t/unify-builds-for-otp-erts-targets/1419)
