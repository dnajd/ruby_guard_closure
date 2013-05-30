# A sample Guardfile
# More info at https://github.com/guard/guard#readme

# settings
@closure_js = ENV['closure_js'].to_s
@guard_regex = Regexp.new ENV['guard_regex'].to_s
@closure_output_file = ENV['closure_output_file'].to_s
@closure_compiler = ENV['current_directory'] + '/closure-compiler/compiler.jar'

@closure_cmd1 = "java -jar #{@closure_compiler} --js #{@closure_js} --create_source_map #{@closure_output_file}.map --source_map_format=V3 --js_output_file #{@closure_output_file} --language_in=ECMASCRIPT5"
@closure_cmd2 = "echo //@ sourceMappingURL=#{@clsoure_source_map} >> #{@closure_output_file}"

# guard-shell stanza
guard :shell do
  watch @guard_regex do |m|
  		# first command (wait with thread)
		t = Thread.new do
		  %x[ #{@closure_cmd1} ]
		end
		t.join    
		
		# second command
		%x[ #{@closure_cmd2} ]
	
  end
end