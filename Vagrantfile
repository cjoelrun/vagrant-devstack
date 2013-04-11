# vim: set ft=ruby

pwd = File.expand_path(File.dirname(__FILE__))

cookbooks = "#{pwd}/cookbooks"

tempest_path = [
  ENV['TEMPEST_ROOT_DIR'],
  "#{pwd}/tempest"
]

tempest = tempest_path.select {|el| File.directory? el.to_s}.first

if tempest.nil?
  system("git clone https://github.com/openstack/tempest.git")
end

Vagrant::Config.run do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.customize ["modifyvm", :id, "--memory", "2048"]

  config.vm.network :hostonly, "10.0.5.10"

  config.vm.share_folder("v-tempest", "/opt/stack/tempest", tempest, :nfs => true)

  config.vm.forward_port 80, 8888

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = cookbooks
    chef.log_level = :debug
    chef.run_list = [
      "recipe[git]",
      "recipe[vim]",
      "recipe[cookbook-devstack]"
    ]
  end
end
