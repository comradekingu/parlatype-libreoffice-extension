project('parlatype-libreoffice-extension',
	version: '3.0',
	#meson_version: '>= 0.47.2', # oldest working tested version
	license: 'GPL3+',
)

app_id  = 'org.parlatype.LibreOfficeExtension'
version = meson.project_version()
bundled = get_option('bundled')
i18n    = import('i18n')
prefix  = get_option('prefix')
base_lo_dir = get_option('libreoffice-dir')

gettext_package = 'parlatype'


python_utils_dir = join_paths(meson.current_source_dir(), 'extension', 'python', 'components', 'pythonpath')

if bundled
	subdir('appdata')
endif
subdir('extension')
subdir('po')
subdir('tests')

if not bundled
	oxt = find_program('create_oxt.sh', required: true)
	zip = find_program('zip', required: true)
	custom_target(
		'oxt',
		command: [ oxt, meson.source_root(), meson.build_root() ],
		output: [ 'Parlatype.oxt' ],
		depends: [ description, options_dialog, toolbar, window_state ],
		build_by_default: true
	)
endif


status = [
  '', '',
  'Parlatype LibreOffice Extension @0@'.format(meson.project_version()),
  ''
]
if bundled
	status += [
  'Mode ............. : bundled',
  'Prefix ........... : @0@'.format(prefix),
  'LibreOffice base.. : @0@'.format(base_lo_dir)
]
else
	status += [
  'Mode ............. : .oxt',
]
endif

status += [ '' ]

message('\n '.join(status))
