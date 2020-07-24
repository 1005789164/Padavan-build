THISDIR = $(shell pwd)
SRC_NAME = smartdns-Release31
S_VERSION := Release31
S_URL := https://codeload.github.com/pymumu/smartdns/tar.gz/$(S_VERSION)

all: download_s extract_test config_test
	$(MAKE) -C $(SRC_NAME)

download_s:
	( if [ ! -f $(THISDIR)/$(SRC_NAME).tar.gz ]; then \
	curl --create-dirs -L $(S_URL) -o $(THISDIR)/$(SRC_NAME).tar.gz ; \
	fi )

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar zxf $(SRC_NAME).tar.gz ; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		touch config_done; \
	fi )

clean:
	rm -rf $(SRC_NAME) config_done

romfs:
	$(ROMFSINST) -p +x $(THISDIR)/$(SRC_NAME)/src/smartdns /usr/bin/smartdns
	$(ROMFSINST) -p +x $(THISDIR)/smartdns.sh /usr/bin/smartdns.sh
	$(ROMFSINST) /etc_ro/smartdns_address.conf
	$(ROMFSINST) /etc_ro/smartdns_blacklist-ip.conf
	$(ROMFSINST) /etc_ro/smartdns_custom.conf
	$(ROMFSINST) /etc_ro/smartdns_whitelist-ip.conf
