# Rakefile tutorial: http://jasonseifer.com/2010/04/06/rake-tutorial
require 'rake'
require 'yaml'

# init settings.yaml
task :init do
	# clean up
	file_name = "settings.yml"
	File.delete(file_name) if File.exist?(file_name)

	# create settings file
	settings = {
		'guard_regex' => '.*test.*', 
		'closure_js' => '*test*',
		'closure_output_file' => 'zscript.closure.js', 
		'watchdir' => '../path_to_watch'
	}
	File.open(file_name, "w") do |file|
  		file.write settings.to_yaml
	end

	# instructions
	puts ''
	puts 'SUCCESS'
	puts 'We created a settings.yaml'
	puts 'Edit this file to configure google closure compile'
	puts ''
	puts 'guard_regex - regex guard uses to find changed files'
	puts 'closure_js - pattern used by closure to find js files to compile'
	puts 'closure_output_file - file name you want google closure to output'
	puts 'watchdir - path to watchdir starting from this project'
	puts ''
end

# loads settings into environment
task :load_settings do

	# settings
	settings = YAML::load_file "settings.yml"
	ENV['guard_regex'] = settings['guard_regex']
	ENV['closure_js'] = settings['closure_js']
	ENV['closure_output_file'] = settings['closure_output_file']
	ENV['watchdir'] = settings['watchdir']

	# current directory
	ENV['current_directory'] = File.dirname(__FILE__)
end

# guard closure task
task :guard_closure do

	# settings
	Rake::Task[:load_settings].invoke

	# start guard
	cmd = "bundle exec guard --watchdir '#{ENV['watchdir']}' --guardfile '#{ENV['current_directory']}/Guardfile'"
	%x[ #{cmd} ]
end	

# example rake task
task :default do

	# two arguments passed to rake task
	# watchdir - path to watchdir starting from this project
	# guardfile - path to this project's guardfile starting from watchdir
  	Rake::Task[:guard_closure].invoke(nil, nil)

end


