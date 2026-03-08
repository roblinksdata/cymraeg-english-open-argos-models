.PHONY: all

HUGGING_FACE_TRANSFORMERS_MODEL := techiaith/mt-dspec-legislation-en-cy
JSON_METADATA_FILES_SOURCE		= $(wildcard argos-package-metadata/*.json)
METADATA_FILES					= $(JSON_METADATA_FILES_SOURCE:argos-package-metadata/%=en-cy/%) en-cy/README.md

MODEL_FILES						:= en-cy/model/shared_vocabulary.json en-cy/model/model.bin en-cy/model/config.json en-cy/sentencepiece.model

all: en-cy.zip

en-cy.argosmodel: en-cy.zip
	cp $< $@

en-cy.zip: $(METADATA_FILES) $(MODEL_FILES) en-cy/stanza
	zip en-cy.zip $(shell find en-cy | xargs)

en-cy/%.json: argos-package-metadata/%.json en-cy
	cp $< $@

en-cy/README.md: argos-package-metadata/README.md en-cy
	cp $< $@

en-cy:
	mkdir -p en-cy

$(MODEL_FILES):
# 	poetry install
# 	<https://opennmt.net/CTranslate2/guides/transformers.html#marianmt>
	poetry run ct2-transformers-converter --model $(HUGGING_FACE_TRANSFORMERS_MODEL) --copy_files source.spm --output_dir en-cy/model
	mv en-cy/model/source.spm en-cy/sentencepiece.model

en-cy/stanza:
	poetry run python -c 'import stanza; stanza.download("en", model_dir="en-cy/stanza", processors="tokenize")'

clean:
	rm -rf en-cy
	rm en-cy.zip