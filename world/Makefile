BRANCH := $(shell git symbolic-ref --short HEAD)
VERSION := $(shell echo $(BRANCH) | sed -E 's/^release\/[^@]+@//')
.SILENT:
.PHONY: _is-release-branch
_is-release-branch:
	if [ ! "$(shell echo $(BRANCH) | grep -E "^release\/[^@]+@[0-9]+\.[0-9]+\.[0-9]+$$")" ]; then \
		echo "Error: Current branch name does not match to /^release\/[^@]+@[0-9]+\.[0-9]+\.[0-9]+$/"; \
		exit 1; \
	fi

.SILENT:
.PHONY: _version-file
_version-file: _is-release-branch
	echo $(VERSION) > VERSION

.SILENT:
.PHONY: _version-readme
_version-readme: _is-release-branch
	sed -i -E 's/(https\:\/\/img\.shields\.io\/badge\/version\-)([0-9]+\.[0-9]+\.[0-9]+)/\1$(VERSION)/g' ./README.md
	sed -i -E 's/(https\:\/\/github\.com\/takuyahara\/test-monorepo-workflows\/releases\/tag\/world%40)([0-9]+\.[0-9]+\.[0-9]+)/\1$(VERSION)/g' ./README.md

.SILENT:
.PHONY: version
version: _version-file _version-readme
	echo Current version: $(VERSION)
