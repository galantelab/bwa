project('bwa', 'c',
          version : '0.7.17',
          license : 'GPL3',
    meson_version : '>= 0.48.0',
  default_options : ['warning_level=0', 'c_std=c99']
)

common_flags = [
  '-D_DEFAULT_SOURCE',
  '-DUSE_MALLOC_WRAPPERS',
  '-DHAVE_PTHREAD'
]

add_project_arguments(common_flags, language : 'c')

cc = meson.get_compiler('c')
m_dep = cc.find_library('m', required : false)
rt_dep = cc.find_library('rt', required : false)

thread_dep = dependency('threads')

zlib_dep = dependency('zlib', fallback : ['zlib', 'zlib_dep'])

deps = [
  thread_dep,
  zlib_dep,
  rt_dep,
  m_dep
]

src = files(
  'bamlite.c',
  'bntseq.c',
  'bwa.c',
  'bwamem.c',
  'bwamem_extra.c',
  'bwamem_pair.c',
  'bwape.c',
  'bwase.c',
  'bwaseqio.c',
  'bwashm.c',
  'bwtaln.c',
  'bwt.c',
  'bwtgap.c',
  'bwt_gen.c',
  'bwtindex.c',
  'bwt_lite.c',
  'bwtsw2_aux.c',
  'bwtsw2_chain.c',
  'bwtsw2_core.c',
  'bwtsw2_main.c',
  'bwtsw2_pair.c',
  'example.c',
  'fastmap.c',
  'is.c',
  'kopen.c',
  'kstring.c',
  'ksw.c',
  'kthread.c',
  'main.c',
  'malloc_wrap.c',
  'maxk.c',
  'pemerge.c',
  'QSufSort.c',
  'rle.c',
  'rope.c',
  'utils.c'
)

headers = files(
  'bamlite.h',
  'bntseq.h',
  'bwa.h',
  'bwamem.h',
  'bwase.h',
  'bwtaln.h',
  'bwtgap.h',
  'bwt.h',
  'bwt_lite.h',
  'bwtsw2.h',
  'kbtree.h',
  'khash.h',
  'kseq.h',
  'ksort.h',
  'kstring.h',
  'ksw.h',
  'kvec.h',
  'malloc_wrap.h',
  'QSufSort.h',
  'rle.h',
  'rope.h',
  'utils.h'
)

extern_incdir = '.include'

# /fullpath/extern_incdir/bwa
install_extern_incdir = join_paths(meson.current_source_dir(), extern_incdir, 'bwa')

message('Creating bwa headers')
run_command('install', '-t', install_extern_incdir, headers, check : true)

inc = include_directories('.')
extern_inc = include_directories(extern_incdir)

bwa = static_library('bwa', src,
  include_directories : inc,
         dependencies : deps,
     override_options : ['warning_level=0', 'c_std=c99'],
              install : false
)

bwa_dep = declare_dependency(
  include_directories : extern_inc,
            link_with : bwa,
              version : meson.project_version()
)
