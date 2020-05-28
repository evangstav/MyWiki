# AWS

# Setting up a jupyter environment in AWS

## Launch AWS instance
1. Under find services select EC2
2. Click Launch Instance
3. (Opt) select free tier (750 hours/month)
4. Create Key pair
5. Launch Instances
6. View Instances

## Connecting to the EC2 instance
ssh -i "pemfile"

## Setting up jupyter
1. sudo yum install -y python37
2. get pip: curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
3. sudo python3 get-pip.py
4. pip install --user jupyter

## Make jupyter accesible remotely
1. Select Security Groups
2. Click Actions -> Edit Inbound Rules(or ad new security group)
3. Add a new rule: change the port to 8888, select "my IP"
4. jupyter notebook --ip <local-ip>
