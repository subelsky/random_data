%w[rubygems rake rake/clean fileutils newgem rubigen].each { |f| require f }
require File.dirname(__FILE__) + '/lib/random_data'

# Generate all the Rake tasks
# Run 'rake -T' to see list of generated tasks (from gem root directory)
$hoe = Hoe.new('random_data', RandomData::VERSION) do |p|
  p.developer('Mike Subelsky', 'mike@subelsky.com')
  p.changes              = p.paragraphs_of("History.txt", 0..1).join("\n\n")
  p.rubyforge_name       = "random-data"
  p.description = "A Ruby gem that provides a Random class with a series of methods for generating random test data including names, mailing addresses, dates, phone numbers, e-mail addresses, and text."
  p.summary = "A Ruby gem that provides a Random class with a series of methods for generating random test data including names, mailing addresses, dates, phone numbers, e-mail addresses, and text."
  p.email = 'random_data@mikeshop.net'
  # p.remote_rdoc_dir = 'random-data'

  # p.extra_deps         = [
  #   ['activesupport','>= 2.0.2'],
  # ]
  p.extra_dev_deps = [
    ['newgem', ">= #{::Newgem::VERSION}"]
  ]
  
  p.clean_globs |= %w[**/.DS_Store tmp *.log]
  path = (p.rubyforge_name == p.name) ? p.rubyforge_name : "\#{p.rubyforge_name}/\#{p.name}"
  p.remote_rdoc_dir = File.join(path.gsub(/^#{p.rubyforge_name}\/?/,''), 'rdoc')
  p.rsync_args = '-av --delete --ignore-errors'
end

require 'newgem/tasks' # load /tasks/*.rake
Dir['tasks/**/*.rake'].each { |t| load t }

desc 'Publish RDoc as website to RubyForge.'
task :publish_docs => [:clean, :docs] do
  local_dir  = 'doc'
  host       = website_config["host"]
  host       = host ? "#{host}:" : ""
  remote_dir = File.join(website_config["remote_dir"])
  sh %{rsync -aCv #{local_dir}/ #{host}#{remote_dir}}
end

# TODO - want other tests/tasks run by default? Add them to the list
# task :default => [:spec, :features]