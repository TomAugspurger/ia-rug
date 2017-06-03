.PHONY: serve

slides.html: slides.md template-revealjs.html
	pandoc -t html5 --template=template-revealjs.html \
		--standalone --section-divs \
		--variable theme="beige" \
		--variable transition="linear" \
		slides.md -o slides.html

serve:
	python3 -m http.server
