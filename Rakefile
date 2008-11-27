require 'tasks/helpers'

tasks_glob = 'tasks/*'
tasks = Dir.glob(tasks_glob)
full_tasks = tasks.inject(Hash.new {|_,_| fail}) {|h,f| h[f] = File.expand_path(f); h}
p full_tasks
def each_task_dir
  Dir.chdir('..') do
    Dir.glob('*').select {|f| FileTest.directory?(f)}.each do |dir|
      Dir.chdir(dir) do
        yield
      end
    end
  end
end

task :diff => :default do
  each_task_dir do
    Dir.glob(tasks_glob).each do |f|
      if tasks.find {|t| t == f}
        out "diff #{File.expand_path(f)} #{full_tasks[f]}"
      end
    end
  end
end
#module-import/tasks/gregproject.rake methodchain/tasks/gregproject.rake
