# How to build TKLamp PDF/HTML manuals from Markdown

## Table of Content

<!-- MarkdownTOC -->

- [Requirements](#requirements)
- [Recommended Markdown editor and linter](#recommended-markdown-editor-and-linter)
- [Build](#build)
    - [PDF](#pdf)
    - [HTML](#html)
    - [DOC](#doc)

<!-- /MarkdownTOC -->

## Requirements

- pandoc : <https://pandoc.org/installing.html>
- esvogel : <https://github.com/Wandmalfarbe/pandoc-latex-template>
- Linux :  
    - TexLive with core, fonts, latex
- Windows (untested, I use Arch Linux) :  
    - MiKTeX

## Recommended Markdown editor and linter

Auto-updates the Markdown TOC, fixes errors to produce the best possible
HTML and PDF, and improves various quality of life features.

- Sublime Text
- Sublime Text Plugins :
    - MarkdownTOC
    - MarkdowPreview
    - MarkdowLivePreview
    - SublimeLinter
    - SublimeLinter-contrib-markdownlint
        - markdownlint-cli
    - Pandoc plugin

## Build

### PDF

```bash
export REPO=TKlamp
sed -E -i 's#\(docs/manual\.md\)#(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/manual.md)#g' README.md
sed -E -i 's#\(docs/serial_data_reference\.md\)#(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/serial_data_reference.md)#g' README.md
pandoc README.md \
docs/manual.md \
docs/serial_data_reference.md \
--data-dir=/usr/share/pandoc/data \
--resource-path=docs \
-f markdown -t pdf \
--template eisvogel \
--listings \
-V book \
-o README.pdf 
sed -E -i 's#\(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/serial_data_reference\.md\)#(docs/serial_data_reference.md)#g' README.md
sed -E -i 's#\(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/manual\.md\)#(docs/manual.md)#g' README.md
```

### HTML

- --css=styling-benjam.css \
- --css=styling-killercup.css \

```bash
export REPO=TKlamp
sed -E -i 's#\(docs/manual\.md\)#(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/manual.md)#g' README.md
sed -E -i 's#\(docs/serial_data_reference\.md\)#(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/serial_data_reference.md)#g' README.md
sed -E -i 's#\.\./res/([^)]+)#https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/res/\1?raw=true#g' docs/manual.md
pandoc README.md \
docs/manual.md \
docs/serial_data_reference.md \
--css=styling-benjam.css \
-s \
-V lang=en \
-V highlighting-css= \
-V linkcolor:blue \
--mathjax \
--resource-path=docs \
-f markdown -t html5 \
--toc \
-o README.html
sed -E -i 's#https://github\.com/'"$REPO"'/TKlamp-Docs/blob/main/res/#../res/#g' docs/manual.md
sed -E -i 's#\(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/serial_data_reference\.md\)#(docs/serial_data_reference.md)#g' README.md
sed -E -i 's#\(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/manual\.md\)#(docs/manual.md)#g' README.md
```

### DOC

```bash
export REPO=TKlamp
sed -E -i 's#\(docs/manual\.md\)#(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/manual.md)#g' README.md
sed -E -i 's#\(docs/serial_data_reference\.md\)#(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/serial_data_reference.md)#g' README.md
pandoc README.md \
docs/manual.md \
docs/serial_data_reference.md \
--resource-path=docs \
-f markdown -t docx \
-V geometry:margin=1.5cm \
--toc \
-V linkcolor:blue \
-o README.docx
sed -E -i 's#\(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/serial_data_reference\.md\)#(docs/serial_data_reference.md)#g' README.md
sed -E -i 's#\(https://github.com/'"$REPO"'/TKlamp-Docs/blob/main/docs/manual\.md\)#(docs/manual.md)#g' README.md
```

---

That's all folks.

I use Arch btw :)

--class101
