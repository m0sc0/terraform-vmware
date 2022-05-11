### Creacion de una vm en Vcenter
sh '''
terraform apply -var "user@vsphere.local" -var "vsphere_password=XXX." -var "vsphere_server=foo.com"
'''

### Main.tf
sh ´´´
[semperti@localhost Terraform]$ vi main.tf
  memory   =  8192
  guest_id = "other3xLinux64Guest"

  network_interface {
    network_id = data.vsphere_network.network.id
  }

  disk {
    label = "disk0"
    size  = 50
  }
}
resource "vsphere_virtual_machine" "vm2" {
  name             = "tanzu-prometheus"
  resource_pool_id = data.vsphere_resource_pool.pool.id
  datastore_id     = data.vsphere_datastore.datastore.id

  num_cpus = 4
  memory   = 16384
  guest_id = "other3xLinux64Guest"

  network_interface {
    network_id = data.vsphere_network.network.id
  }
  disk {
    label = "disk0"
    size  = 500
  }
}
resource "vsphere_virtual_machine" "vm3" {
  name             = "tanzu-thanos"
  resource_pool_id = data.vsphere_resource_pool.pool.id
  datastore_id     = data.vsphere_datastore.datastore.id

  num_cpus = 4
  memory   = 16384
  guest_id = "other3xLinux64Guest"

  network_interface {
    network_id = data.vsphere_network.network.id
  }
  disk {
    label = "disk0"
    size  = 500
  }
}
´´´
