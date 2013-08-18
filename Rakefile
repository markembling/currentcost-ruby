require 'rake'
require 'spec'
require 'rspec/core/rake_task'
require 'rdoc/task'
require 'rubygems/specification'
require 'rubygems/package_task'

task :default => [:spec]

RSpec::Core::RakeTask.new do |t|
  t.pattern = './spec/**/*_spec.rb'
  #t.rcov = true
  #t.rcov_opts = ['--exclude', 'spec'] 
end

Rake::RDocTask.new { |rdoc|
  rdoc.rdoc_dir = 'doc'
  rdoc.title    = "CurrentCost-Ruby - RDoc documentation"
  rdoc.options << '--line-numbers' << '--inline-source' << '-A cattr_accessor=object'
  rdoc.options << '--charset' << 'utf-8'
  rdoc.rdoc_files.include('README', 'COPYING')
  rdoc.rdoc_files.include('lib/**/*.rb')
}

# Gem build task - load gemspec from file
gemspec = File.read('currentcost-ruby.gemspec')
spec = nil
# Eval gemspec in SAFE=3 mode to emulate github build environment
Thread.new { spec = eval("$SAFE = 3\n#{gemspec}") }.join
Gem::PackageTask.new(spec) do |p|
  p.gem_spec = spec
end