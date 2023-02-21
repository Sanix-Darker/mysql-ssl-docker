
FROM debian:jessie

RUN  apt-get update && apt-get install -y openssl

# In the "openssl req" commands these options prevent
# any prompts from the user:
#
#   -notes does not encrypt the certificates, 
#        hence no need for a password
#   -subj "/C=US/ST=Denial/L=Springfield/O=Dis/CN=www.example.com"
#        supplies the identification information
#
# From: https://superuser.com/questions/226192/avoid-password-prompt-for-keys-and-prompts-for-dn-information

# The X509 identifier must differ by CN value
# https://stackoverflow.com/questions/19726138/openssl-error-18-at-0-depth-lookupself-signed-certificate#19738223

ENV OPENSSL_SUBJ="/C=US/ST=California/L=Santa Clara"
ENV OPENSSL_CA="${OPENSSL_SUBJ}/CN=fake-CA"
ENV OPENSSL_SERVER="${OPENSSL_SUBJ}/CN=fake-server"
ENV OPENSSL_CLIENT="${OPENSSL_SUBJ}/CN=fake-client"

COPY gencerts.sh /
RUN chmod +x /gencerts.sh

VOLUME /certs

WORKDIR /certs

CMD /gencerts.sh
