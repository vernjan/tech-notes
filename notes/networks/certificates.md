# Certificates

- decoding cetificates https://www.sslshopper.com/certificate-decoder.html
    - `openssl x509 -in cert.crt -text -noout`

## CSR - Certificate Signing Request

- **goal**: to obtain a signed certificate from CA
- process
    - generate private key (RSA, ECC, ..)
        - `openssl genrsa -out key.pem 2048`
    - generate CSR
        - `openssl req -new -key www.ssls.cz.key -out www.ssls.cz.csr`
        - provide **common name**, country, organization info, email, ...
    - send CSR to CA
    - CA issues the certificate