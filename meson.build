project('pywin32', ['c', 'cpp'])

swig = find_program('swig')
windmc = find_program('windmc')

python_dep = dependency('python3')

subdir('win32')
subdir('com')

swig_gen = generator(swig,
  output : '@BASENAME@module.cpp',
  arguments : [
    '-I@SOURCE_DIR@/SWIG/swig_lib/python',
    '-I@SOURCE_DIR@', 
    '-python', 
    '-c++', 
    '-o', '@OUTPUT@', 
    '@INPUT@',
  ],
)

win32_swig_src = swig_gen.process(win32_swig)

windmc_gen = generator(windmc,
  output  : ['@BASENAME@.h', '@BASENAME@.rc'],
  arguments : '@INPUT@',
)

win32_mc_gen = windmc_gen.process(win32_mc)

library('win32',
  [win32_mc_gen, win32_src],
  include_directories : [win32_inc],
  dependencies : python_dep,
  cpp_args : [
    '-DBUILD_PYWINTYPES', 
    '-DCRYPT_DECRYPT_MESSAGE_PARA_HAS_EXTRA_FIELDS',
  ],
)
