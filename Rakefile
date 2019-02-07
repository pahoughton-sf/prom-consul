# 2018-10-13 (cc) <paul4hough@gmail.com>
#

# 2018-10-10 (cc) <paul4hough@gmail.com>
#
# y = rake recurses down (. .. ../..:)

$runstart = Time.now

at_exit {
  runtime = Time.at(Time.now - $runstart).utc.strftime("%H:%M:%S.%3N")
  puts "run time: #{runtime}"
}

task :default do
  sh 'rake --tasks'
  exit 1
end

# task :galaxy do
#   sh "ansible-galaxy install -r require-roles.yml -p roles"
# end

task :yamllint do
  sh "yamllint -f parsable ."
end

task :ansible_syntax do |task, args|
  sh "ansible-playbook --syntax-check " + \
     "--list-tasks ansible/node-prom.yml -i prom,"
  sh "ansible-playbook --syntax-check " + \
     "--list-tasks ansible/node-anode.yml -i anode,"
end

task :test => [:yamllint, :ansible_syntax]

task :up, [:node] => [:test] do |task, args|
  sh "vagrant #{task} #{args[:node]}"
end

task :provision, [:node] => [:test] do |task, args|
  sh "vagrant #{task} #{args[:node]}"
end


# task :test, [:backend] do | task, args|
#   Dir.chdir('testinfra') do
#     sh "py.test -v"
#   end
# end
