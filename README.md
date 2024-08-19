# WebTransportTestConnection

This repo show a simple code that allows to open a webtransport session from a browser to a webtransport local server. It shows how you can create self signed certificate that will be trusted by the browser to connect to a localhost server.

**That is very nice if you want to test your webtransport implementation against a server running in localhost**

# Test

- Clone this repo
```
git clone git@github.com:jordicenzano/WebTransportTestConnection
```

- Create key, certificate, and certificate fingerprint by running following script
```
./create_self_signed_certs.sh
```
The trick here is that this script will create a self signed certificate for localhost with EDCSA and validity of 10 days (<15)

- Run your webtransport server using the key and certificate generated in the previous step
In out case we used MOQ server [moxygen](https://github.com/facebookexperimental/moxygen)
```
./_build/bin/moqrelayserver -port 4433 -cert ../WebTransportTestConnection/certs/certificate.pem -key ../WebTransportTestConnection/certs/certificate.key -endpoint "/moq" --logging DBG
```

- Run local webserver by
Starts webserver in port 8080
```
./start_webserver.py
```

- Open test webpage and hit "Connect"
If all works as expected you should see a log indicating "WT connection OPENED!"

# Thanks
Thanks to Luke Curley pointers and his example in [moq-rs](https://github.com/kixelated/moq-rs/blob/main/dev/cert)
