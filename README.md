easycert openssl
===============

This provides an easy automated way to create your own certificate authority including a root certificate, intermediate certificate, and server certificate using openssl all in one command.

Downloading
===========

    $ curl -O https://raw.github.com/jsermeno/kerl/master/easycert
    $ chmod a+x easycert

Add the easycert file to your $PATH. Note: openssl command is a prerequisite.

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

There will be several prompts. You will need to enter passphrases for your root key and intermediate key and re-enter these passphrases when prompted, so do not forget them. You will also be prompted if you want to override the values specified in the config. If you want to keep them the same you can just press `enter` and your default value will be used. Note: The organization value must be the same for your certificates.

This will create the directory structure for your own certificate authority and all necessary certificates. There is also a command for quickly printing the paths to your certificates and server key.

    $ easycert find ~/.ca
    ca:                /Users/jsermeno/.ca/certs/ca.cert.pem
    intermediate:      /Users/jsermeno/.ca/intermediate/certs/intermediate.cert.pem
    server key:        /Users/jsermeno/.ca/intermediate/private/localhost.key.pem
    server:            /Users/jsermeno/.ca/intermediate/certs/localhost.cert.pem
    ca-chain:          /Users/jsermeno/.ca/intermediate/certs/ca-chain.cert.pem
    done.

You're set! Include your server cert and server key on your server. Include your ca-chain cert on the client.

Customization
============
The `easycert` file is just a bash script. At the very least it provides documentation for how to operate this flow using openssl. Go into the file and make changes if you need to change the encryption or other options.

Credit
======
Credit to [jamielinux](https://jamielinux.com/articles/2013/08/act-as-your-own-certificate-authority/) for the basis of this script. This was the closest source of information outside of the openssl docs that was even close to working. This got me 90% of the way there. Unfortunately, there are a couple of mistakes that prevent the entire flow from working correctly.
