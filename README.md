# Certificate authority - How to be one in own network

When you have multiple services on your network which are using self-signed certificates   
it can be cumbersome to always add an exception for the self signed certificate for every website.   
To avoid that, you can add your own CA root certificate to your systems trusted ca certificates,   
which will be used to sign all networks services certificats. With this all services certs will be trusted,   
aslong the self created CA cert is imported to the current machine.   
The CA cert chain must be imported only once to every machine and all signed certs with it will be trusted as well.

Steps for CA root:
- `ca_steps.md`
  - `field_values.md` can be used as a reference to answer questions asked by openssl
Steps for clients/machines:
- `client_steps.md`
Steps for servers/services:
- `server_steps.md`
  - `field_values.md` can be used as a reference to answer questions asked by openssl
