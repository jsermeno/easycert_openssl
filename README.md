easycert openssl
===============

This provides an easy automated way to create your own certificate authority including a root certificate, intermediate certificate, and server certificate all in one command.

Downloading
===========

    $ curl -O https://raw.github.com/jsermeno/kerl/master/easycert
    $ chmod a+x easycert

Add the easycert file to your $PATH

Usage
====

The most difficult part is creating a configuration file. Copy the following into the shell. The most important part is `EASYCERT_COMMON_NAME`. This needs to match your domain.

    $ cat > ~/.easycertrc << EOF
    EASYCERT_COUNTRY="US"
    EASYCERT_STATE="California"
    EASYCERT_LOCALITY="Mountain View"
    EASYCERT_ORGANIZATION="Catchvar"
    EASYCERT_UNIT="Studio"
    EASYCERT_COMMON_NAME="localhost"
    EASYCERT_EMAIL="catchvar@gmail.com"
    EASYCERT_UNSTRUCTURED="Catchvar"
    EOF

Then just run one command specifying where you want your certificate authority to be created.

    $ easycert create-all ~/.ca

This will create the directory structure for your own certificate authority and all necessary certificates. There is also a command for quickly printing the paths to your certificates and server key.

    $ easycert find ~/.ca




