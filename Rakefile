class Ansible
  def self.playbook(tags)
    cmd  = %Q{ANSIBLE_FORCE_COLOR=true ansible-playbook}
    cmd += %Q{ -i mybtcnode,}
    cmd += %Q{ playbook.yml}
    cmd += %Q{ --tags "#{Array(tags).join ','}"} if tags != []
    cmd += %Q{ --extra-vars "@config.json"}
    # cmd += %Q{ -vvv} # Uncomment for max verboseness
    puts cmd
    run cmd
  end

  def self.run(cmd)
    IO.popen "ANSIBLE_FORCE_COLOR=true #{cmd}" do |io|
      while (line = io.gets) do
        puts line
      end
    end
  end
end

namespace :mybtcnode do
  desc "Install dependencies"
  task :install_dependencies do
    Ansible.playbook 'dependencies'
  end

  desc "Set hostname"
  task :hostname do
    Ansible.playbook 'hostname'
  end

  desc "Set up security"
  task :security do
    Ansible.playbook 'security'
  end

  desc "Set up bitcoin_classic"
  task :bitcoin_classic do
    Ansible.playbook 'bitcoin_classic'
  end

  desc "Get info"
  task :get_info do
    Ansible.playbook 'get_info'
  end

  desc "Sets up everything"
  task :setup do
    Ansible.playbook %w{dependencies hostname security bitcoin_classic get_info}
  end
end
