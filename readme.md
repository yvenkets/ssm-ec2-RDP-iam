#Access EC2 instance via ssm and access rdp in local machine.
create iam ec2-ssm role
attach this two policies

AmazonSSMManagedInstanceCore
AmazonSSMFullAccess


launch the ec2 instance with this ami
Windows_Server-2016-English-Full-Base-2022

attach the role  to the instance


start the seesion with session manager

other wise inatall ssm clinet on that vm

install aws clin in your local pc

configure aws credentials in that pc 

execute the commands in the session manager windows or your local power shell

to access the ec2 using ssm in your local powershell

                  aws ssm start-session --target instance-id

create the user and add to remote desktop group

    $Password = Read-Host -AsSecureString
	
	New-LocalUser "User01" -Password $Password
	
	Add-LocalGroupMember -Group "Remote Desktop Users" -Member "User01"

port forwarding

aws ssm start-session \
    --target instance-id \
    --document-name AWS-StartPortForwardingSession \
    --parameters '{"portNumber":["80"], "localPortNumber":["56789"]}'
	
	
Now you can access the ec2 in your local pc mstsc 

localhost:56789




