require 'rake'
require 'rake/clean'
require 'rake/testtask'
require 'rdoc/task'
require 'rubygems/package_task'

task :default => [:compile, :test]

CLEAN.add "geoip.{o,bundle,so,obj,pdb,lib,def,exp}"
CLOBBER.add ['Makefile', 'mkmf.log','doc']

RDoc::Task.new do |rdoc|
  rdoc.main = "README.md" # page to start on
  rdoc.rdoc_files.include("README.md", "ext/geoip/geoip.c")
  rdoc.rdoc_dir = 'doc/' # rdoc output folder
end

Rake::TestTask.new do |t|
  t.test_files = ['test.rb']
  t.verbose = true
end

spec = Gem::Specification.load "geoip-c.gemspec"

Gem::PackageTask.new(spec) do |pkg|
  pkg.need_tar = true
end

desc 'compile the extension'
task(:compile => 'Makefile') { sh 'make' }
file('Makefile' => "geoip.c") { ruby 'extconf.rb' }

task :install => [:gem] do
  `env ARCHFLAGS="-arch i386" gem install pkg/geoip-c-0.5.0.gem -- --with-geoip-dir=/usr/local/GeoIP`
end

task(:webpage) do
  sh 'scp -r doc/* rydahl@rubyforge.org:/var/www/gforge-projects/geoip-city/'
end
