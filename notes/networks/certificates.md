# Certificates

- decoding certificates https://www.sslshopper.com/certificate-decoder.html
    - `openssl x509 -in CERT_FILE -text -noout`
- decoding bundle certificates (a file with multiple certificates)
    - `openssl storeutl -noout -text -certs vasaRoot.crt`
- decoding RSA keys
    - `openssl rsa -in KEY_FILE -text -noout`

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