ANOLIS		= anolis
SED  = sed
CURL  = curl
SPECSTOP	= ..
GENDIR		= $(SPECSTOP)/cssom
XREF  = data
XREFS		= $(XREF)/xrefs/css/cssom-view.json
SRCFILE  = Overview.src.html
VNUFILE  = Overview.src.vnu.html
EDFILE		= Overview.html
TRFILE		= TR/Overview.html

all: $(EDFILE) $(XREFS)

$(XREFS): Overview.src.html Makefile
	$(ANOLIS) --dump-xrefs=$@ $< /tmp/spec; $(RM) /tmp/spec

$(EDFILE): Overview.src.html $(XREF) Makefile
	$(ANOLIS) --output-encoding=utf-8 --omit-optional-tags --quote-attr-values --use-strict \
	--w3c-compat-substitutions --w3c-compat-xref-a-placement --enable=xspecxref --w3c-compat-class-toc --enable=refs --w3c-shortname="cssom-view" \
	--filter=".publish" $< $@; \
 $(SED) 's/\[/\(/g;s/\]/\)/g' <$(SRCFILE) >$(VNUFILE); \
 $(CURL) -F out=gnu -F content=@$(VNUFILE) http://html5.validator.nu/; \
 $(RM) $(VNUFILE); \
 $(CURL) 'http://www.w3.org/2009/07/webidl-check?doc=http%3A%2F%2Fdev.w3.org%2Fcsswg%2Fcssom-view%2F&output=text'
 #$(CURL) -F output=text -F input=@$(SRCFILE) http://www.w3.org/2009/07/webidl-check

draft: $(EDFILE)

$(TRFILE): Overview.src.html $(XREF) Makefile
	$(ANOLIS) --output-encoding=utf-8 --omit-optional-tags --quote-attr-values --use-strict \
	--w3c-compat-substitutions --w3c-compat-xref-a-placement --enable=xspecxref --w3c-compat-class-toc --enable=refs --w3c-shortname="cssom-view" \
	--filter=".dontpublish" --pubdate="$(PUBDATE)" \
 --w3c-status=WD $< $@

publish: $(TRFILE)
