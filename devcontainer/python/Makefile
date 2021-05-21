SHELL := /bin/bash


### LINT

lint: lint-md lint-md-link lint-md-spell lint-python

lint-md:
	$(info Starting markdownlint)
	markdownlint '**/*.md'

lint-md-link:
	$(info Starting markdown-link-check)
	find . -name \*.md -print0 | xargs -n 1 -0 markdown-link-check -c .markdownlinkcheck.json

lint-md-spell:
	$(info Starting mdspell)
	mdspell --en-us --ignore-acronyms --ignore-numbers  '**/*.md' --report

lint-python:
	$(info Starting flake8)
	flake8 .
	black -check -l 120 .
	# flake8 ./src
	# flake8 ./tests
	# black --check -l 120 ./src
	# black --check -l 120 ./tests