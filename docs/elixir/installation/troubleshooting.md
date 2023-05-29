# Troubleshooting

## Installing an Old Version of Erlang if OpenSSL 1.1.1 is missing

Build OpenSSL from sources

    cd /usr/local/src/
    sudo git clone https://github.com/openssl/openssl.git -b OpenSSL_1_1_1-stable openssl-1.1.1m
    cd openssl-1.1.1m
    sudo ./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl shared zlib
    sudo make
    sudo make test
    sudo make install_sw

Install Erlang

    KERL_CONFIGURE_OPTIONS="--with-ssl=/usr/local/openssl-1.1.1" asdf install erlang 23.3
