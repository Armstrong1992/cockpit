LINGUAS = de da pl

basedir = $(pkgdatadir)/base1
base_GEN = \
	$(addprefix po/po.,$(addsuffix .js,$(LINGUAS))) \
	$(NULL)
base_GZ = \
	pkg/base1/angular.min.js.gz \
	pkg/base1/cockpit.min.css.gz \
	pkg/base1/po.js.gz \
	pkg/base1/require.min.js.gz \
	pkg/base1/term.min.js.gz \
	pkg/base1/mustache.min.js.gz \
	pkg/base1/jquery.min.js.gz \
	pkg/base1/cockpit.min.js.gz \
	pkg/base1/bundle.min.js.gz \
	$(base_GEN:.js=.js.gz) \
	$(NULL)
base_DATA = \
	pkg/base1/manifest.json \
	$(base_GZ) \
	$(NULL)

basedebugdir = $(debugdir)$(basedir)
basedebug_DATA = \
	pkg/base1/angular.js \
	pkg/base1/cockpit.css \
	pkg/base1/patternfly.css \
	pkg/base1/po.js \
	pkg/base1/require.js \
	pkg/base1/patterns.js \
	pkg/base1/term.js \
	pkg/base1/mustache.js \
	pkg/base1/jquery.js \
	pkg/base1/cockpit.js \
	$(base_GEN) \
	$(NULL)

base_BUNDLE = \
	pkg/base1/require.min.js \
	pkg/base1/cockpit.min.js \
	pkg/base1/jquery.min.js \
	pkg/base1/mustache.min.js \
	pkg/base1/patterns.min.js \
	$(NULL)

pkg/base1/bundle.min.js: $(base_BUNDLE)
	$(AM_V_GEN) $(srcdir)/tools/missing $(srcdir)/tools/jsbundle $@ $^
pkg/base1/term.min.js: pkg/base1/term.js
	@$(MKDIR_P) $(dir $@)
	$(AM_V_GEN) $(srcdir)/tools/missing $(srcdir)/tools/uglifyjs $< --mangle > $@.tmp && $(MV) $@.tmp $@

install-data-local::
	$(MKDIR_P) $(DESTDIR)$(basedebugdir)
	$(LN_S) -f require.js $(DESTDIR)$(basedebugdir)/bundle.js

basefontsdir = $(pkgdatadir)/base1/fonts
basefonts_DATA = \
	pkg/base1/fonts/fontawesome.woff.gz \
	pkg/base1/fonts/patternfly.woff.gz \
	pkg/base1/fonts/glyphicons.woff.gz \
	$(NULL)

basefontsdebugdir = $(debugdir)$(basefontsdir)
basefontsdebug_DATA = \
	pkg/base1/fonts/fontawesome.woff \
	pkg/base1/fonts/patternfly.woff \
	pkg/base1/fonts/glyphicons.woff \
	$(NULL)

base_TESTS = \
	pkg/base1/test-base64.html \
	pkg/base1/test-utf8.html \
	pkg/base1/test-chan.html \
	pkg/base1/test-echo.html \
	pkg/base1/test-async.html \
	pkg/base1/test-no-jquery.html \
	pkg/base1/test-spawn.html \
	pkg/base1/test-spawn-proc.html \
	pkg/base1/test-http.html \
	pkg/base1/test-dbus.html \
	pkg/base1/test-dbus-framed.html \
	pkg/base1/test-location.html \
	pkg/base1/test-framed.html \
	pkg/base1/test-locale.html \
	pkg/base1/test-format.html \
	pkg/base1/test-file.html \
	pkg/base1/test-metrics.html \
	pkg/base1/test-user.html \
	pkg/base1/test-time.html \
	pkg/base1/test-permissions.html \
	pkg/base1/test-series.html \
	pkg/base1/test-cache.html \
	pkg/base1/test-framed-cache.html \
	$(NULL)

TESTS += $(base_TESTS)

CLEANFILES += \
	pkg/base1/bundle.min.js \
	pkg/base1/term.min.js \
	pkg/base1/cockpit.min.js \
	pkg/base1/patterns.min.js \
	$(base_GEN) \
	$(base_GZ) \
	$(NULL)

EXTRA_DIST += \
	pkg/base1/angular.min.js \
	pkg/base1/bundle.min.js \
	pkg/base1/jquery.min.js \
	pkg/base1/require.min.js \
	pkg/base1/mustache.min.js \
	pkg/base1/term.min.js \
	$(base_BUNDLE) \
	$(base_DATA) \
	$(basedebug_DATA) \
	$(baseimages_DATA) \
	$(basefonts_DATA) \
	$(basefontsdebug_DATA) \
	$(base_TESTS) \
	$(NULL)

update-lib:: update-bower
	$(srcdir)/tools/uglifyjs \
		$(BOWER)/patternfly/components/bootstrap-combobox/js/bootstrap-combobox.js \
			> bootstrap-combobox.min.js
	$(srcdir)/tools/uglifyjs $(BOWER)/jquery-flot/jquery.flot.js > jquery.flot.min.js
	$(srcdir)/tools/uglifyjs $(BOWER)/jquery-flot/jquery.flot.selection.js > jquery.flot.selection.min.js
	$(srcdir)/tools/uglifyjs $(BOWER)/jquery-flot/jquery.flot.time.js > jquery.flot.time.min.js
	$(srcdir)/tools/uglifyjs $(BOWER)/jquery-amend/jquery-amend.js > jquery-amend.min.js
	sed -f $(srcdir)/tools/patternfly.sed \
		$(BOWER)/patternfly/dist/css/patternfly.css > patternfly.css
	$(JSMODULE) -o $(srcdir)/pkg/base1/jquery.js \
	    $(BOWER)/jquery/dist/jquery.js \
	    $(BOWER)/patternfly/components/bootstrap/dist/js/bootstrap.js \
	    $(BOWER)/patternfly/components/bootstrap-select/bootstrap-select.js \
	    $(BOWER)/bootstrap-datepicker/dist/js/bootstrap-datepicker.js \
	    $(BOWER)/patternfly/components/bootstrap-combobox/js/bootstrap-combobox.js \
	    $(BOWER)/patternfly/dist/js/patternfly.js \
	    $(BOWER)/jquery-flot/jquery.flot.js \
	    $(BOWER)/jquery-flot/jquery.flot.selection.js \
	    $(BOWER)/jquery-flot/jquery.flot.time.js \
	    $(BOWER)/jquery-amend/jquery-amend.js \
	    $(srcdir)/pkg/base1/jquery-scoped.js \
	    $(srcdir)/pkg/base1/attrchange.js
	$(JSMODULE) -o $(srcdir)/pkg/base1/jquery.min.js \
	    $(BOWER)/jquery/dist/jquery.min.js \
	    $(BOWER)/patternfly/components/bootstrap/dist/js/bootstrap.min.js \
	    $(BOWER)/patternfly/components/bootstrap-select/bootstrap-select.min.js \
	    $(BOWER)/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js \
	    bootstrap-combobox.min.js \
	    $(BOWER)/patternfly/dist/js/patternfly.min.js \
	    jquery.flot.min.js \
	    jquery.flot.selection.min.js \
	    jquery.flot.time.min.js \
	    jquery-amend.min.js \
	    $(srcdir)/pkg/base1/jquery-scoped.js \
	    $(srcdir)/pkg/base1/attrchange.min.js
	$(srcdir)/tools/uglifyjs $(BOWER)/requirejs/require.js > require.min.js
	$(JSMODULE) -o $(srcdir)/pkg/base1/require.js \
	    $(BOWER)/requirejs/require.js \
	    $(srcdir)/pkg/base1/require-config.js \
	    $(srcdir)/pkg/base1/require-loaders.js
	$(JSMODULE) -o $(srcdir)/pkg/base1/require.min.js \
	    require.min.js \
	    $(srcdir)/pkg/base1/require-config.js \
	    $(srcdir)/pkg/base1/require-loaders.js
	$(srcdir)/tools/cssbundle -o $(srcdir)/pkg/base1/patternfly.css \
	    patternfly.css \
	    $(BOWER)/bootstrap-datepicker/dist/css/bootstrap-datepicker.css
	$(JSMODULE) -o $(srcdir)/pkg/base1/mustache.js \
		$(BOWER)/mustache/mustache.js
	$(srcdir)/tools/uglifyjs $(BOWER)/mustache/mustache.js > \
		$(srcdir)/pkg/base1/mustache.min.js
	$(JSMODULE) -m -a window.Terminal -o $(srcdir)/pkg/base1/term.js \
	    $(BOWER)/term.js/src/term.js
	cp $(BOWER)/patternfly/dist/fonts/PatternFlyIcons-webfont.woff \
		$(srcdir)/pkg/base1/fonts/patternfly.woff
	cp $(BOWER)/patternfly/components/bootstrap/fonts/glyphicons-halflings-regular.woff \
		$(srcdir)/pkg/base1/fonts/glyphicons.woff
	cp $(BOWER)/patternfly/components/font-awesome/fonts/fontawesome-webfont.woff \
		$(srcdir)/pkg/base1/fonts/fontawesome.woff
	$(JSMODULE) -m -a window.angular -o $(srcdir)/pkg/base1/angular.js \
	    $(BOWER)/angular/angular.js \
	    $(BOWER)/angular-route/angular-route.js \
	    $(BOWER)/angular-bootstrap/ui-bootstrap.js
	$(JSMODULE) -m -a window.angular -o $(srcdir)/pkg/base1/angular.min.js \
	    $(BOWER)/angular/angular.min.js \
	    $(BOWER)/angular-route/angular-route.min.js \
	    $(BOWER)/angular-bootstrap/ui-bootstrap.min.js

# Never recreate these files
pkg/base1/angular.min.js:
	@true
pkg/base1/jquery.min.js:
	@true
pkg/base1/mustache.min.js:
	@true
pkg/base1/require.min.js:
	@true
