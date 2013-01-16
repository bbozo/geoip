require 'rake'
require 'rake/clean'
require 'rake/testtask'
require 'rdoc/task'
require 'rubygems/package_task'
require "rake/extensiontask"

task :default => [:compile, :test]

CLOBBER.add 'doc'

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

Rake::ExtensionTask.new("geoip", spec) do |ext|
end

task(:webpage) do
  sh 'scp -r doc/* rydahl@rubyforge.org:/var/www/gforge-projects/geoip-city/'
end
