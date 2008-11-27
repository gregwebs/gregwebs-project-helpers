require 'tasks/helpers'

def each_project_dir &block
  Dir.chdir('..') do
    Dir.glob('*').select {|f| FileTest.directory?(f)}.each do |dir|
      Dir.chdir(dir, &block)
    end
  end
end

tasks_glob = 'tasks/*'
tasks = Dir.glob(tasks_glob).sort

desc "diff"
task :diff do
  full_tasks = tasks.inject(Hash.new {|_,_| fail}) do |h,f|
    h[f] = File.expand_path(f)
    h
  end

  each_project_dir do
    Dir.glob(tasks_glob).each do |f|
      if tasks.find {|t| t == f}
        out "diff #{File.expand_path(f)} #{full_tasks[f]}"
      end
    end
  end
end

desc "commit"
task :commit do
  each_project_dir do |dir|
    modified = `git status | grep modified | awk '{print $3}'`.split($/).sort
    if !modified.empty? && (modified - tasks).empty?
      puts dir
      out 'git commit -a -m ', "'update project helpers'"
    end
  end
end
#module-import/tasks/gregproject.rake methodchain/tasks/gregproject.rake
