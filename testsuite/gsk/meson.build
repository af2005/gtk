testexecdir = join_paths(installed_test_bindir, 'gsk')
testdatadir = join_paths(installed_test_datadir, 'gsk')

test_render_nodes = executable(
  'test-render-nodes',
  ['test-render-nodes.c',
   'reftest-compare.c'],
  dependencies: libgtk_dep,
  install: get_option('install-tests'),
  install_dir: testexecdir
)

cairo_test_env = environment()
cairo_test_env.set('G_TEST_SRCDIR', meson.current_source_dir())
cairo_test_env.set('G_TEST_BUILDDIR', meson.current_build_dir())
cairo_test_env.set('GSETTINGS_BACKEND', 'memory')
cairo_test_env.set('G_ENABLE_DIAGNOSTIC', '0')
cairo_test_env.set('GSK_RENDERER', 'cairo')

test('nodes (cairo)', test_render_nodes,
             args: [ '--tap', '-k' ],
             env: cairo_test_env,
             suite: 'gsk')

vulkan_test_env = environment()
vulkan_test_env.set('G_TEST_SRCDIR', meson.current_source_dir())
vulkan_test_env.set('G_TEST_BUILDDIR', meson.current_build_dir())
vulkan_test_env.set('GSETTINGS_BACKEND', 'memory')
vulkan_test_env.set('G_ENABLE_DIAGNOSTIC', '0')
vulkan_test_env.set('GSK_RENDERER', 'vulkan')

test('nodes (vulkan)', test_render_nodes,
     args: [ '--tap', '-k' ],
     env: vulkan_test_env,
     suite: 'gsk')

test_data = [
  'blendmode.node',
  'blendmode.png',
  'blendmode.vulkan.png',
  'blendmodes.node',
  'blendmodes.png',
  'blendmodes.vulkan.png',
  'cairo.node',
  'cairo.png',
  'colors.cairo.png',
  'colors.node',
  'colors.vulkan.png',
  'cross-fade.node',
  'cross-fade.png',
  'cross-fades.node',
  'cross-fades.png',
  'cross-fades.vulkan.png',
  'ducky.png',
  'repeat.node',
  'repeat.png',
  'transform.node',
  'transform.png',
  'transform.vulkan.png',
]

if get_option('install-tests')
  conf = configuration_data()
  conf.set('libexecdir', gtk_libexecdir)
  configure_file(input: 'render-nodes-cairo.test.in',
                 output: 'render-nodes-cairo.test',
                 configuration: conf,
                 install_dir: testdatadir)
  configure_file(input: 'render-nodes-vulkan.test.in',
                 output: 'render-nodes-vulkan.test',
                 configuration: conf,
                 install_dir: testdatadir)

  install_data(test_data, install_dir: testexecdir)

endif
