project('json-glib', 'c',
  version : '1.2.3',
  meson_version : '>= 0.35.0',
  default_options : [ 'warning_level=1',
                      'buildtype=debugoptimized' ])


# Versionning
json_version = meson.project_version()
version_arr = json_version.split('.')
json_version_major = version_arr[0]
json_version_minor = version_arr[1]
json_version_micro = version_arr[2]
if version_arr.length() == 4
  json_version_nano = version_arr[3]
else
  json_version_nano = 0
endif

apiversion = '1.0'
soversion = 0

# maintaining compatibility with the previous libtool versioning
# current = minor * 100 + micro
libversion = '@0@.@1@.0'.format(soversion, json_version_minor.to_int() * 100 + json_version_micro.to_int())

# Dependencies
glib_req_version = '>= 2.37.6'
gobject_dep = dependency('gobject-2.0', version : glib_req_version)
gio_dep = dependency('gio-2.0', version : glib_req_version)

# Configurations
cc = meson.get_compiler('c')
cdata = configuration_data()

check_headers = [
  ['dlfcn.h','HAVE_DLFCN_H'],
  ['unistd.h', 'HAVE_UNISTD_H'],
  ['sys/types.h', 'HAVE_SYS_TYPES_H'],
  ['sys/stat.h', 'HAVE_SYS_STAT_H'],
  ['string.h', 'HAVE_STRING_H'],
  ['strings.h', 'HAVE_STRINGS_H'],
  ['stdint.h', 'HAVE_STDINT_H'],
  ['memory.h', 'HAVE_MEMORY_H'],
  ['inttypes.h', 'HAVE_INTTYPES_H'],
  ['dlfcn.h','HAVE_DLFCN_H'],
]

foreach h : check_headers
  if cc.has_header(h.get(0))
    cdata.set(h.get(1), 1)
  endif
endforeach

check_functions = [
  ['HAVE_DCGETTEXT', 'dcgettext', '#include<libintl.h>'],
]
foreach f : check_functions
  if cc.has_function(f.get(1), prefix : f.get(2))
    cdata.set(f.get(0), 1)
  endif
endforeach

cdata.set_quoted('GETTEXT_PACKAGE', 'json-glib-1.0')
cdata.set_quoted('PACKAGE_BUGREPORT', 'http://bugzilla.gnome.org/enter_bug.cgi?product=json-glib')
cdata.set_quoted('PACKAGE_NAME', 'json-glib')
cdata.set_quoted('PACKAGE_STRING', 'json-glib ' + json_version)
cdata.set_quoted('PACKAGE_URL', 'http://live.gnome.org/JsonGlib')
cdata.set_quoted('PACKAGE_VERSION', json_version)
# FIXME Check how to do it with mingw
cdata.set('_JSON_EXTERN', '__attribute__((visibility("default"))) extern')

configure_file(input : 'config.h.meson',
  output : 'config.h',
  configuration : cdata)

root_dir = include_directories('.')
gnome = import('gnome')
subdir('json-glib')
