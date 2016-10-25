-include Makeinclude.mk
DOCS=index 
HTMLDIR=..
HDOCS=$(addsuffix .html, $(DOCS))
PHDOCS=$(addprefix $(HTMLDIR)/, $(HDOCS))

.PHONY : docs
docs : $(PHDOCS)

CONF=
$(HTMLDIR)/index.html : CONF+=-c mysite.conf

$(HTMLDIR)/%.html : %.jemdoc
	jemdoc.py $(CONF) -o $@ $<

.PHONY : update-stanford
update-stanford : $(PHDOCS)
	@echo -n 'Copying to server...'
	rsync -vr $(HTMLDIR)/* --exclude .git* --exclude src $(STAN_SERVER)
	@echo ' done.'

.PHONY : clean
clean :
	-rm -f $(HTMLDIR)/*.html
