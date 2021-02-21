#Cert-Manager
We use cert-manager to issue our ssl certificates used by our internal applications.

## Installation
Because cert-manager checks that the `_acme-challenge` TXT DNS entry is successfully created before actually issuing the certification process,
we have to use a different DNS server, in our case Quad9 (9.9.9.9).

Execute the following commands for a successfull installation:

    helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.2.0 --set installCRDs=true --set 'extraArgs={--dns01-recursive-nameservers-only,--dns01-recursive-nameservers=9.9.9.9:53}'
    kubectl apply -f digitalocean-dns-secret.yaml    
    kubectl apply -f cluster-issuer.yaml

## Test
The included certificate.yaml can be used to check for a working cert-manager instance.

    kubectl apply -f certificate.yaml
