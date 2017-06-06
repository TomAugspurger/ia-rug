.PHONY: serve

slides.html: slides.md template-revealjs.html
	pandoc -f markdown \
		-t html5 \
		--template=template-revealjs.html \
		--standalone --section-divs \
		--variable theme="black" \
		--variable transition="none" \
		slides.md -o slides.html

serve:
	python3 -m http.server
