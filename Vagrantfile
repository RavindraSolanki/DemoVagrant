Vagrant.configure('2') do |config|
    vagrant_username = 'vagrant'
    vagrant_password = 'Welcome2018!'

    config.vm.box = 'azure'
    config.vm.communicator = "winrm"
    config.winrm.username = vagrant_username
    config.winrm.password = vagrant_password
    config.ssh.username = vagrant_username
    config.ssh.password = vagrant_password

    config.vm.provider :azure do |azure, override|
        azure.tenant_id = ENV['AZURE_TENANT_ID']
        azure.client_id = ENV['AZURE_CLIENT_ID']
        azure.client_secret = ENV['AZURE_CLIENT_SECRET']
        azure.subscription_id = ENV['AZURE_SUBSCRIPTION_ID'] #to get this run: azure account list

        ##to get this run: azure vm image list --location westeurope --publisher MicrosoftWindowsServer
        azure.instance_ready_timeout = 600
        
        azure.vm_image_urn = 'MicrosoftWindowsServer:WindowsServerSemiAnnual:Datacenter-Core-1803-with-Containers-smalldisk:1803.0.20180613'
        azure.vm_size = 'Standard_B1s'
        azure.vm_name = 'vagrantdemowin' # max 15 characters. contains letters, number and hyphens. can start with letters and can end with letters and numbers
        
        azure.location = 'westeurope' # to select location run: azure location list
        azure.resource_group_name = 'VagrantGroup'
        azure.nsg_name = 'vagrantnsg' # Network Security Group Name

        azure.admin_username = vagrant_username # defaults to 'vagrant' if not provided
        azure.admin_password = vagrant_password # min 8 characters. should contain a lower case letter, an uppercase letter, a number and a special character
        azure.winrm_install_self_signed_cert = true
        
        override.vm.guest = :windows
        override.winrm.transport = :ssl
        override.winrm.port = 5986
        override.winrm.ssl_peer_verification = false # must be false if using a self signed cert
        override.vm.synced_folder ".", "/vagrant", disabled: true
  end

end
