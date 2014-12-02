
ENV = development

CSS := $(find lib -name '*.css' -print)
HTML := $(find lib -name '*.html' -print)
JS := $(find lib -name '*.js' -print)
JSON := $(find lib -name '*.json' -print)

default: build

beautify: $(JS)
	@js-beautify --replace $(JS)

build: components $(CSS) $(HMTL) $(JS)
	@bin/build-client \
		--env $(ENV) \
		--out build

components: $(JSON)
	@component install --dev

install: node_modules
	@npm install -g component js-beautify jshint serve

lint: $(JS)
	@jshint $(JS)

node_modules: package.json
	@npm install

.PHONY: beautify install lint
