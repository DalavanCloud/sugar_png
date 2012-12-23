# encoding: utf-8

require 'rubygems'
require 'bundler'
begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  $stderr.puts e.message
  $stderr.puts "Run `bundle install` to install missing gems"
  exit e.status_code
end
require 'rake'

require 'jeweler'
Jeweler::Tasks.new do |gem|
  # gem is a Gem::Specification... see http://docs.rubygems.org/read/chapter/20 for more options
  gem.name = "sugar_png"
  gem.homepage = "http://github.com/zed-0xff/sugar_png"
  gem.license = "MIT"
  gem.summary = %Q{a syntax sugar of PNG manipulation}
  #gem.description = %Q{TODO: longer description of your gem}
  gem.email = "zed.0xff@gmail.com"
  gem.authors = ["Andrey \"Zed\" Zaikin"]
  gem.executables = %w'sugar_png'
  gem.files.include "lib/**/*.rb"
  # dependencies defined in Gemfile
end
Jeweler::RubygemsDotOrgTasks.new

require 'rspec/core'
require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = FileList['spec/**/*_spec.rb']
end

RSpec::Core::RakeTask.new(:rcov) do |spec|
  spec.pattern = 'spec/**/*_spec.rb'
  spec.rcov = true
end

task :default => :spec

desc "generate"
task :gen do
  $:.unshift("./lib")
  require 'sugar_png'
  img = ZPNG::Image.new :width => 16, :height => 16, :bpp => 4
  img.save "out.png"
end

Rake::Task[:console].clear

# from /usr/local/lib64/ruby/gems/1.9.1/gems/jeweler-1.8.4/lib/jeweler/tasks.rb
desc "Start IRB with all runtime dependencies loaded"
task :console, [:script] do |t,args|
  dirs = ['./ext', './lib'].select { |dir| File.directory?(dir) }

  original_load_path = $LOAD_PATH

  cmd = if File.exist?('Gemfile')
          require 'bundler'
          Bundler.setup(:default)
        end

  # add the project code directories
  $LOAD_PATH.unshift(*dirs)

  # clear ARGV so IRB is not confused
  ARGV.clear

  require 'irb'

  # ZZZ actually added only these 2 lines
  require 'sugar_png'
  include ZPNG

  # set the optional script to run
  IRB.conf[:SCRIPT] = args.script
  IRB.start

  # return the $LOAD_PATH to it's original state
  $LOAD_PATH.reject! { |path| !(original_load_path.include?(path)) }
end
