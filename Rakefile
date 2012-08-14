PUPPETMASTER = 'ip-10-244-141-201'
SSH='ssh -t -A'

task :deploy do
  sh "git push git@github.com:denishpatel/postgres-puppet.git"
  sh "#{SSH} #{PUPPETMASTER} 'cd /etc/puppet && sudo git pull git@github.com:denishpatel/postgres-puppet.git'"
end

task :apply => [:deploy] do
   client = ENV['CLIENT']
   sh "#{SSH} #{client} 'sudo puppet agent --test'" do |ok,
   status|
       puts case status.exitstatus
           when 0 then "Client is up to dat."
           when 1 then "Puppet coudn't compile the manifest."
           when 2 then "Puppet made changes."
           when 4 then "Puppet found errors"
       end
    end
end 
