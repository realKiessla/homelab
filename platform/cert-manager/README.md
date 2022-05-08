# Cert-Manager
We use cert-manager to issue our ssl certificates used by our internal applications.

## Extension / Customization
Because cert-manager checks that the `_acme-challenge` TXT DNS entry is successfully created before actually issuing the certification process,
we have to use a different DNS server, in our case Quad9 (9.9.9.9).
