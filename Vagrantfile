# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "perk/ubuntu-2204-arm64"
  config.vm.provider "qemu" do |qe|
    qe.memory = "1G"
    qe.net_device = nil
  end

  (0..1).each do |i|
    config.vm.define "controller-" + i.to_s do |controller|
      controller.vm.provider "qemu" do |qe|
        qe.ssh_port = 50022 + i
        qe.extra_qemu_args = [
          "-device", "virtio-net-device,netdev=net0",
          "-netdev", "user,id=net0,hostfwd=tcp::" + (50022 + i).to_s + "-:22",
          "--device", "virtio-net-pci,netdev=net1,mac=9E:E3:BF:36:47:8" + i.to_s,
          "--netdev", "vmnet-shared,id=net1"
        ]
      end
    end
  end
end
