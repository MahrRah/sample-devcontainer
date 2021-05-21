SHELL := /bin/bash


### LINT

lint: lint-md lint-md-link lint-md-spell lint-js

lint-md:
	$(info Starting markdownlint)
	markdownlint '**/*.md'

lint-md-link:
	$(info Starting markdown-link-check)
	find . -name \*.md -print0 | xargs -n 1 -0 markdown-link-check -c .markdownlinkcheck.json

lint-md-spell:
	$(info Starting mdspell)
	mdspell --en-us --ignore-acronyms --ignore-numbers  '**/*.md' --report

lint-js:
	$(info Starting flake8)
