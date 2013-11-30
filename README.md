#Sensu client playbook

Playbook to install and configure a sensu-server. This is a work in progress,
it will come with various configuration tweaking later on :)

##Supported system

Currently only Debian Jessie amd64 is supported and tested. Patch welcome to
support other OS.

##Installation

Just clone (or submodule) this repository under the name `sensu-server` in your
`roles` directory. This file, `test.yml` and `Vagrantfile` will be ignored by
ansible anyway.

###Using it

####Variables

You may need to redefine the following variables:

|Name|Type|Description|Default|
|----|----|-----------|-------|
`sensu_client_hostname`|String|Hostname of this client|`"localhost"`
`sensu_client_address`|String|Address of this client|`"127.0.0.1"`
`sensu_client_subscription_names`|List|List of test to execute on this client| `[test]`
`sensu_server_rabbitmq_hostname`|String|Hostname of the RabbitMQ server (Master Node)|`"localhost"`
`sensu_server_rabbitmq_user`|String|Username used for RabbitMQ|`"sensu"`
`sensu_server_rabbitmq_password`|String|Password for the RabbitMQ user|`"placeholder"`

####Files

You have to put the needed certificates in your `files/` folder, those will be
used to encrypt the communication between your different host:

    files/
     |- sensu_client_cert.pem
     |- sensu_client_key.pem

Please note that the `files` folder of this repository contains dummy
certificate. You should **not** use them. Your certificate will get precedence
over the ones of this role if put in your root `files` folder.

##Test

There is some really basic tests with the playbook. It just try to install
rabbitmq in a vagrant VM. Just run:

    $ vagrant up

and the VM will be provisioned by ansible with the test.yml.
