NULL =

GENERATED_ITEMS =	\
	json-glib.vcproj	\
	json-glib-install.vsprops

json-glib-install.vsprops: $(top_srcdir)/build/win32/vs9/json-glib-install.vspropsin json-glib.headers
	$(CPP) -P - <$(top_srcdir)/build/win32/vs9/json-glib-install.vspropsin >$@
	rm json-glib.headers

EXTRA_DIST =	\
	json-glib.sln			\
	json-glib-version-paths.vsprops	\
	json-glib-build-defines.vsprops	\
	json-glib-gen-srcs.vsprops	\
	json-glib-install.vspropsin	\
	json-glib.vcprojin		\
	json-glib-validate.vcproj	\
	json-glib-format.vcproj	\
	json-glib-install.vcproj	\
	README.txt			\
	array.vcproj			\
	boxed.vcproj			\
	builder.vcproj			\
	generator.vcproj		\
	gvariant.vcproj			\
	invalid.vcproj		\
	node.vcproj			\
	object.vcproj			\
	parser.vcproj			\
	path.vcproj			\
	reader.vcproj			\
	serialize-complex.vcproj	\
	serialize-full.vcproj		\
	serialize-simple.vcproj		\
	$(GENERATED_ITEMS)		\
	$(NULL)

DISTCLEANFILES = $(GENERATED_ITEMS)
