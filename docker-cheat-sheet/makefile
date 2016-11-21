basename = docker-cheat-sheet

all: build

build:
	asciidoctor $(basename).adoc

pdf:
	asciidoctor-pdf $(basename).adoc

clean:
	rm -f $(basename).html
	rm -f $(basename).pdf
