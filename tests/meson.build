# Copyright 2018 Endless Mobile, Inc.

javascript_tests = [
    'libanimations-dbus/testClient.js',
]

jasmine = find_program('jasmine')
test_runner = find_program('./tap.py')
include_path = '@0@:@1@'.format(meson.source_root(), meson.build_root())
built_library_path = join_paths(meson.build_root(), meson.project_name())
test_content_path = join_paths(meson.current_source_dir(), 'testcontent')
tests_environment = environment()
tests_environment.set('GJS_PATH', include_path)
tests_environment.prepend('GI_TYPELIB_PATH', built_library_path)
tests_environment.prepend('LD_LIBRARY_PATH', built_library_path)
tests_environment.set('G_TEST_SRCDIR', meson.current_source_dir())
tests_environment.set('G_TEST_BUILDDIR', meson.current_build_dir())
tests_environment.prepend('XDG_DATA_DIRS', test_content_path)
tests_environment.set('LC_ALL', 'C')

args = [jasmine.path(), '--no-config', '--tap']
if (jasmine_report_argument != '')
    args += [jasmine_report_argument]
endif

foreach test_file : javascript_tests
    srcdir_file = join_paths(meson.current_source_dir(), test_file)
    test(test_file, test_runner, env: tests_environment,
        args: args + [srcdir_file])
endforeach
