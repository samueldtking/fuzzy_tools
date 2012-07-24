require 'bundler'
Bundler::GemHelper.install_tasks

Dir[File.expand_path('../accuracy/**/*.task', __FILE__)].each { |f| load f }
Dir[File.expand_path('../performance/**/*.task', __FILE__)].each { |f| load f }

task :default => :test

require 'rspec/core/rake_task'
desc "Run the tests"
RSpec::Core::RakeTask.new(:test)

desc "Launch an IRB session with the gem required"
task :console do
  $:.unshift(File.dirname(__FILE__) + '/../lib')

  require 'fuzzy_tools'
  require 'irb'

  IRB.setup(nil)
  irb = IRB::Irb.new

  IRB.conf[:MAIN_CONTEXT] = irb.context

  irb.context.evaluate("require 'irb/completion'", 0)

  trap("SIGINT") { irb.signal_handle }
  catch(:IRB_EXIT) { irb.eval_input }
end