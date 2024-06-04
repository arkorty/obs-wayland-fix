project('wlrobs', 'c', default_options : ['buildtype=release', 'warning_level=2'])

cc = meson.get_compiler('c')

inc = include_directories('inc')
wayland = dependency('wayland-client')
obs = dependency('libobs')
dl = cc.find_library('dl')

sources = ['src/main.c', 'proto/xdg-output-unstable-v1-protocol.c']

deps = [wayland, obs, dl]

if get_option('use_scpy')
	sources += ['src/scpy_source.c', 'proto/wlr-screencopy-unstable-v1-protocol.c']
	deps += cc.find_library('rt')
	add_project_arguments('-DENABLE_SCPY', language : 'c')
endif

if get_option('use_dmabuf')
	sources += ['src/dmabuf_source.c', 'proto/wlr-export-dmabuf-unstable-v1-protocol.c']
	add_project_arguments('-D_GNU_SOURCE', '-DENABLE_DMABUF', language : 'c')
endif

shared_library(
	meson.project_name(),
	sources,
	include_directories : inc,
	dependencies : deps,
	install : true,
	install_dir : get_option('libdir') / 'obs-plugins'
)
