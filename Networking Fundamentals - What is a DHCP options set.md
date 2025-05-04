What is DHCP ?
It stands for Dynamic Host Configuration Protocol
It assists in auto configuration for network resources

Lets explain that in more details as to what it means :

DHCP Server in the network establishes a connection with the device, which is the dhcp client through layer 2 broadcast
Upon establishing the connection , the dhcp client, the device in this case, receives IP address, Subnet Mask and Default Gateway

So how it relates to networking in the cloud ?
When we refer to networking in the cloud, we mean the VPC - VIrtual Private cloud

AWS has its own DNS server , AmazonProvidedDNS which maps to Route 53 resolver
Every resource within the vpc is alloted a private dns domain and a public dns domain name ( if the resources is configured to have a public IP )

DHCP option sets

The option sets are immutable
DHCP options are set  to a VPC
VPC can be associated to a single dhcp option set only
DHCP in general is how a device receives an IP address, subnect mask and default gate way. The same is true for resources created within a vpc as well
IP address within a  vpc is allocated automatically, subnet mask is derived from the vcp cidr range and default gateway always maps to subnet + 1 adress
So, what can we configure with dhcp option set within a vpc - It is the DNS service to use
This is the route 53 resolver--vpc + 2 address

NTP service is time synchronization is important

format of DNS names which are allotted to resources within a vpc

private dns name - ip-private-ipv4-address.region.compute.internal
public dns name - ec2-public-ipv4-address.region.compute.amazonaws.com

Lets look at it by way of illustration : 
I have a VPC and have created 3 Ec2 instances
I want to use a custom dns server and have a domain name of myapp.local

So, we create a dhcp options set with following values :
domain-name = myapp.local
domain-name-servers = 10.0.0.10

We will associate these dhcp options set at the VPC level so that all resources created within the vpc receives the same settings

Architecture View :

references : https://docs.aws.amazon.com/vpc/latest/userguide/DHCPOptionSetConcepts.html

![How resources use DHCP](https://github.com/sanchayansen-star/AWS-Cloud-Programming-Foundations/blob/main/dhcp-custom-update-new.png?raw=true)
