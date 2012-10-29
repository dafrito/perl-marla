CA=testca

CERTFILES= \
	cacert.pem \
	private/cakey.pem \
	index.txt \
	index.txt.attr \
	tsaserial

ca: $(addprefix $(CA)/,$(CERTFILES))
.PHONY: ca

$(CA)/cacert.pem: $(CA)/private/cakey.pem | $(CA)
	openssl req -new -batch -x509 -days 3650 -extensions v3_ca \
		-key $< -out $(CA)/cacert.pem

$(CA)/private/cakey.pem: | $(CA)
	openssl genpkey -algorithm rsa -out $@

$(CA)/index.txt $(CA)/index.txt.attr: | $(CA)
	touch $@

$(CA)/tsaserial:
	echo 01 >$@

$(CA):
	mkdir -p $@/private $@/newcerts

clean-ca:
	rm -rf $(CA)
.PHONY: clean-ca

cert: cert.crt
.PHONY: cert

cert.crt: ca cert.csr cert.key
	openssl ca -batch -config $(CA).config -out $@ -infiles cert.csr
.PHONY: cert

cert.csr cert.key:
	openssl req -new -batch -nodes \
		-out $@ \
		-keyout cert.key \
		-config $(CA).config

clean-cert:
	rm -f cert.csr cert.crt cert.key
.PHONY: clean-cert

clean: clean-ca clean-cert
.PHONY: clean
