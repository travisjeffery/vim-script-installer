# written by travis jeffery <github:travisjeffery>

require 'rake'
require 'find'
require 'pathname'

IGNORE = [/\.git/, /^\.\.$/, /^\.$/, /Rakefile$/]

files = []

Find.find(Dir.new(File.dirname(__FILE__)).path) do |path|
  unless IGNORE.any? { |re| path.match(re) } || File.directory?(path)
    files << Pathname.new(path).relative_path_from(Pathname.new(File.dirname(__FILE__))).to_s
  end
end

desc 'Install plugin and documentation'
task :install do
  vimfiles = if ENV['VIMFILES']
               ENV['VIMFILES']
             elsif RUBY_PLATFORM =~ /(win|w)32$/
               File.expand_path("~/vimfiles")
             else
               File.expand_path("~/.vim")
             end
  files.each do |file|
    target_file = File.join(vimfiles, file)
    FileUtils.mkdir_p File.dirname(target_file)
    FileUtils.cp file, target_file

    puts "Installed #{file} to #{target_file}"
  end

end
