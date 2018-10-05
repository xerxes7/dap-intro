# Certificate Generator

Creates certificates to mimic the PKI certificates a customer might find in their own environment.

This script will generate:
- Root key/certificate
- Intermediate key/certificate, signed by Root
- Conjur Node certificates, all signed by the Intermediate:
    - `master-1.mycompany.local`
    - `master-2.mycompany.local`
    - `master-3.mycompany.local`
    - `follower-1.mycompany.local`
    - `follower-2.mycompany.local`

### Generate
To create these certificates, navigate to this directory and run:
```
$ ./generate_certificates
```

You can now use the following certificates to configure a Conjur cluster:
- `certificates/intermediate/cert/ca-chain.cert.pem` - CA Cert
- `certificates/nodes/master-1.mycompany.local/master-1.mycompany.local.cert.pem` - Master cert
- `certificates/nodes/master-1.mycompany.local/master-1.mycompany.local.key.pem` - Master key
- `certificates/nodes/follower-1.mycompany.local/follower-1.mycompany.local.cert.pem` - Follower 1 cert
- `certificates/nodes/follower-1.mycompany.local/follower-1.mycompany.local.key.pem` - Follower 1 key
- `certificates/nodes/follower-2.mycompany.local/follower-2.mycompany.local.cert.pem` - Follower 2 cert
- `certificates/nodes/follower-2.mycompany.local/follower-2.mycompany.local.key.pem` - Follower 2 key

### Customizing
The domain can be customized by changing the following lines in `generate_certificates`:
```
domain='mycompany.local'
nodes=( 'master-1' 'master-2' 'master-3' 'follower-1' 'follower-2' )
altname='DNS:master.mycompany.local'
```

Updating to the following:
```
domain='cyberark.local'
nodes=( 'master' 'follower1' 'follower2' )
altname='DNS:master.cyberark.local'
```
will produce signed certificates for the following domains:
- `master.cyberark.local`
- `follower1.cyberark.local`
- `follower2.cyberark.local`

including the Altname: `master.cyberark.local`