install_header_dir ='json-glib-1.0/json-glib'

source_h = ['json-builder.h', 'json-generator.h',
  'json-gobject.h', 'json-gvariant.h', 'json-parser.h',
  'json-path.h', 'json-reader.h', 'json-types.h',
  'json-utils.h', 'json-version-macros.h']

headers_paths = []
foreach h: source_h
    headers_paths += [meson.current_source_dir() + '/' + h]
endforeach

json_glib_enums = gnome.mkenums('json-enum-types',
  sources : headers_paths,
  h_template : 'json-enum-types.h.in',
  c_template : 'json-enum-types.c.in',
  install_header : true,
  install_dir : get_option('includedir') + '/' + install_header_dir)


source_c = [
  'json-array.c', 'json-builder.c', 'json-debug.c',
  'json-gboxed.c', 'json-generator.c', 'json-gobject.c',
  'json-gvariant.c', 'json-node.c', 'json-object.c',
  'json-parser.c', 'json-path.c', 'json-reader.c',
  'json-scanner.c', 'json-serializable.c', 'json-utils.c',
  'json-value.c',
]

version_data = configuration_data()
version_data.set('JSON_MAJOR_VERSION', json_version_major)
version_data.set('JSON_MINOR_VERSION', json_version_minor)
version_data.set('JSON_MICRO_VERSION', json_version_micro)
version_data.set('JSON_VERSION', meson.project_version())

version_h = configure_file(input : 'json-version.h.in',
  output : 'json-version.h',
  install_dir : get_option('includedir') + '/' + install_header_dir,
  configuration : version_data)

install_headers(source_h, subdir : install_header_dir)

localedir = get_option('localedir')
json_c_args = ['-DJSON_COMPILATION', '-DG_LOG_DOMAIN="Json"', '-DJSON_LOCALEDIR="@0@"'.format(localedir)]
json_lib = library('json_glib-1.0',
    source_c,
    version : libversion,
    soversion : soversion,
    include_directories : root_dir,
    dependencies: [gio_dep, gobject_dep],
    c_args : json_c_args,
    install : true,
)

pkgg = import('pkgconfig')

pkgg.generate(
  libraries : [json_lib],
  subdirs : '.',
  version : json_version,
  name : 'JSON-GLib',
  filebase : 'json-glib-@0@'.format(apiversion),
  description : 'JSON Parser for GLib.',
  requires : 'glib-2.0 gio-2.0'
)

json_glib_dep = declare_dependency(link_with : json_lib,
  include_directories : root_dir,
  dependencies : [gobject_dep, gio_dep],
  # Everything that uses libgst needs this built to compile
  sources : [json_glib_enums, version_h],
)

json_glib_validate = executable('json-glib-validate',
    'json-glib-validate.c',
    c_args : json_c_args,
    dependencies: json_glib_dep)

json_glib_validate = executable('json-glib-format',
    'json-glib-format.c',
    c_args : json_c_args,
    dependencies: json_glib_dep)

subdir('tests')
