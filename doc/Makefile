#  SPDX-License-Identifier: BSD-3-Clause
#  Copyright (C) 2015 Intel Corporation
#  All rights reserved.
#

all: doc
	@:

.PHONY: all doc clean

doc: output

deprecation.md: ../deprecation.md
	$(Q)sed -e 's/^# Deprecation/# Deprecation {#deprecation}/' \
	    < $< > $@

changelog.md: ../CHANGELOG.md
	$(Q)sed -e 's/^# Changelog/# Changelog {#changelog}/' \
	    -e 's/^##/#/' \
	    -e 's/^# \(\(v..\...\):.*\)/# \1 {#changelog-\2}/' \
	    -e '/# v..\...:/s/\./-/2' \
	    < $< > $@

output: Doxyfile changelog.md deprecation.md $(wildcard *.md) $(wildcard ../include/spdk/*.h)
	$(Q)rm -rf $@
	$(Q)doxygen Doxyfile

clean:
	$(Q)rm -rf output changelog.md deprecation.md
