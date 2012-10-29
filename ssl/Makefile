CADIR=testca

CERTFILES= \
	cacert.pem \
	private/cakey.pem \
	index.txt \
	index.txt.attr \
	tsaserial

ca: $(addprefix $(CADIR)/,$(CERTFILES))
.PHONY: ca

$(CADIR)/cacert.pem: $(CADIR)/private/cakey.pem | $(CADIR)
	openssl req -new -batch -x509 -days 3650 -extensions v3_ca \
		-key $< -out $(CADIR)/cacert.pem

$(CADIR)/private/cakey.pem: | $(CADIR)
	openssl genpkey -algorithm rsa -out $@

$(CADIR)/index.txt $(CADIR)/index.txt.attr: | $(CADIR)
	touch $@

$(CADIR)/tsaserial:
	echo 01 >$@

$(CADIR):
	mkdir -p $@/private

clean:
	rm -rf $(CADIR)

.PHONY: clean
