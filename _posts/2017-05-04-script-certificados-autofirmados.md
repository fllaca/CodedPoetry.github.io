---
layout: post
title: "Certificados autofirmados en un comando!"
description: 'Os dejo un script para generar certificados autofirmados en un solo comando '
tags:
- linux 
- certificates
categories:
- Snippets
twitter_text: 'Genera certificados autofirmados en un solo comando!'
---

Crear certificados autofirmados para usar en pruebas o redes privadas suele ser bastante engorroso. Con este script podréis generarlos fácilmente con una sola línea de comando: `./gen-cert.sh mydomain.test`

### Script: gen-cert.sh

{% highlight shell %}

# Usage

# 

# $ ./gen-cert.sh myweb

# Will generate "myweb.crt" and "myweb.key"

CERT\_NAME=$1

# Generate a Private Key

openssl genrsa -des3 -out $CERT\_NAME.key 1024

# Generate a CSR (Certificate Signing Request)

openssl req -new -key $CERT\_NAME.key -out $CERT\_NAME.csr

# Remove Passphrase from Key

cp $CERT\_NAME.key $CERT\_NAME.key.org
openssl rsa -in $CERT\_NAME.key.org -out $CERT\_NAME.key

# Generating a Self-Signed Certificate

openssl x509 -req -days 365 -in $CERT\_NAME.csr -signkey $CERT\_NAME.key -out $CERT\_NAME.crt

echo "Generated Certificates: "
echo " - $CERT\_NAME.key"
echo " - $CERT\_NAME.crt"
echo

{% endhighlight %}