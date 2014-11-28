# -*- mode: ruby -*-
# vi: set ft=ruby :

# Author: Tuomo Tanskanen <tumi@tumi.fi>

Vagrant.configure("2") do |config|

  config.vm.define :gitlab do |config|
    # Vagrant 1.5 type box
    config.vm.box = "chef/ubuntu-14.04"

    # Install CI
    config.vm.provision :shell, :path => "install-gitlab-ci.sh"

    # Expose port 3000 for GitlabCI, use 443 if you manually configure SSL too
    config.vm.network :forwarded_port, guest: 3000, host: 3000
    # config.vm.network :forwarded_port, guest: 443, host: 443

    # CI Runner cannot be automated in a full install as it needs a token from CI
    # Install it (from here to by hand), then go to ~gitlab_ci_runner/gitlab-ci-runner
    # and execute as root: "../register-runner.sh <token>"
    # config.vm.provision :shell, :path => "install-gitlab-ci-runner.sh"
  end

  # GitLab recommended specs
  config.vm.provider "virtualbox" do |v, override|
    v.customize [ "modifyvm", :id, "--cpus", "2" ]
    v.customize [ "modifyvm", :id, "--memory", "2048" ]
  end

  config.vm.provider "vmware_fusion" do |v, override|
    v.vmx["numvcpus"] = "2"
    v.vmx["memsize"] = "2048"
  end

  config.vm.provider "lxc" do |v, override|
    override.vm.box = "fgrehm/precise64-lxc"
  end
end
