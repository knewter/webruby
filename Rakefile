# Webruby Rakefile
# Note this is a full-fledged Rakefile(not minirake-powered)!

BASE_DIR = File.expand_path(File.dirname(__FILE__))
$LOAD_PATH.unshift(File.join(BASE_DIR, *%w[rakelib]))

BUILD_DIR = File.join(BASE_DIR, %w[build])
EMSCRIPTEN_DIR = File.join(BASE_DIR, %w[modules emscripten])
MRUBY_DIR = File.join(BASE_DIR, %w[modules mruby])
APP_DIR = File.join(BASE_DIR, %w[app])
DRIVER_DIR = File.join(BASE_DIR, %w[driver])

CC = File.join(EMSCRIPTEN_DIR, 'emcc')
LD = File.join(EMSCRIPTEN_DIR, 'emcc')
AR = File.join(EMSCRIPTEN_DIR, 'emar')

MRUBY_BUILD_CONFIG = File.join(BASE_DIR, 'build_config.rb')
MRBC = File.join(MRUBY_DIR, %w[build host bin mrbc])
LIBMRUBY = File.join(%w[build emscripten lib libmruby.a])
LIBMRUBY_FILE = File.join(MRUBY_DIR, LIBMRUBY)

# Specify supported loading modes of webruby, see rakelib/functions.rb file
# for details, by default all 3 loading modes are supported
LOAD_MODE = ENV['LOAD_MODE'] || 2

CFLAGS = %w(-DMRB_USE_FLOAT -Wall -Werror-implicit-function-declaration)
CFLAGS << "-I#{MRUBY_DIR}/include"
LDFLAGS = []

load 'app/app.rake'
load 'driver/driver.rake'

# tasks
task :default => :js

task :js => "#{BUILD_DIR}/mruby.js"
task :js_exe => ["#{BUILD_DIR}/mruby_exe.js"]

desc "cleanup"
task :clean do |t|
  sh "cd #{MRUBY_DIR} && CONFIG=#{MRUBY_BUILD_CONFIG} ./minirake clean"
  sh "rm -f #{BUILD_DIR}/app.c #{BUILD_DIR}/app.o #{BUILD_DIR}/rbcode.rb #{BUILD_DIR}/rbcode.c #{BUILD_DIR}/main.o"
  sh "rm -f #{BUILD_DIR}/gem_library.js #{BUILD_DIR}/functions"
  sh "rm -f #{BUILD_DIR}/mruby.js #{BUILD_DIR}/mruby_exe.js"
end
