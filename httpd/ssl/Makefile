CERT=127.0.0.1

cert: $(CERT).crt
.PHONY: $(CERT)

$(CERT).crt: $(CERT).csr $(CERT).key
	openssl req -x509 -key $(CERT).key -in $(CERT).csr -out $@
.PHONY: $(CERT)

$(CERT).csr $(CERT).key:
	openssl req -new -batch -nodes \
		-out $@ \
		-keyout $(CERT).key \
		-config $(CERT).config

clean:
	rm -f $(CERT).csr $(CERT).crt $(CERT).key
.PHONY: clean
