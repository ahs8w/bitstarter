bitstarter
==========

// Setting up Amazon EC2 instance (elastic compute cloud) //

Ubuntu Server 12.04.2 LTS  64bit
  Download key pair
  
Create Security Group
  ssh-http-https
    select rules for ssh, http, https
    select custom TCP rule
      port: 8080
  make sure there are 4 open ports: 22, 80, 443, 8080
  
Launch Instance (after terminating if necessary)
  Edit Details
    Security Settings
      select ssh-http-https
      
Launch

// SSH - connecting to remote EC2 instances //

cd ~/folder_with_pem_file/filename.pem
chmod 400 filename.pem   ->   only user can read the file
ssh -i filename.pem ubuntu@[EC2 Public DNS]

mkdir -p ~/.ssh
cp ~/downloads/filename.pem ~/.ssh/
chmod 400 ~/.ssh/filename.pem
chmod 700 ~/.ssh
nano ~/.ssh/config
  Host awshost1
  HostName [EC2 Public DNS]
  User ubuntu
  IdentityFile "~/.ssh/filename.pem"
  
ssh awshost1

// SCP/Rsync //

scp hello.txt awshost1:~/         
  # copy from local to remote home directory
rsync -avp text.txt awshost1:~/   
  # same as above w/ rsync(copying/creating directories)
scp awshost1:~/foo.txt .          
  # copy from remote to current local directory
scp awshost1:~/foo.txt cc/a.b     
  # copy foo.txt from remote to local directory cc, renaming it a.b
