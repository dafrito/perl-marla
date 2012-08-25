# Site-specific makefile
# Do not run this before ./configure is run.

build:
.PHONY: build

install: $(HTTPDETC)
	mkdir -p $(HTTPDETC)/sites.d
	cp httpd.conf $(HTTPDETC)/sites.d/$(PACKAGE).conf
	# Use [@] to ensure we don't get substitutions
	find $(HTTPDETC) -name '*.conf' | xargs sed -i \
		-e "s/[@]SERVER_NAME@/$(SERVER_NAME)/g" \
		-e "s/[@]PACKAGE@/$(PACKAGE)/g" \
		-e "s/[@]IP@/$(IP)/g" \
		-e "s/[@]PORT@/$(PORT)/g" \
		-e "s/[@]LISTEN_DIRECTIVE@/$(LISTEN_DIRECTIVE)/g"
.PHONY: install

uninstall:
.PHONY: uninstall

clean:
.PHONY: clean
