Google Cloud Fundamentals: Getting Started with Compute Engine
Lab Objectives: Be able to create virtual machines (VMs) instances and connect to them, and create connections between the instances.
Task 1: Sign in to the Google Cloud Platform (GCP) Console
login into Google Cloud using the command below
gcloud auth login
select your project with the command below
gcloud config set project PROJECT\_ID
Task 2: Create a virtual machine
The command below will create a VM named my-vm- in the region us-central11-a of deafault machine type n1-standard-1 with boot disk image Debian GNU/linux 9 (stretch).
gcloud compute instances create my-vm-2 --zone=us-central1-a --machine-type=ni-standard-1 --tags=http

Tagging the VM with an http tag for firewall rule to allow http access.

gcloud compute firewall-rule create default-allow-http --direction=INGRESS --priority=1000 --network=default \\
--action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http
Task 3: Create another virtual machine
Set the default zone to the one different from that of the my-vm-1 with this command
gcloud config set compute/zone us-central1-b

To create a VM instance named my-vm-2 in that zone, execute the following command:
gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" \\
--image "debian-9-stretch-v20190213" --subnet "default"
Task 4: Connect between VM instances
SSH into th VM named my-vm-2 with the following ssh command
ssh my-vm-2
Use the ping command to confirm that my-vm-2 can reach my-vm-2 over the network:
ping my-vm-2

press Ctrl+C to abort
Use the ssh command to open a command prompt on my-vm-2:
ssh my-vm-2
At the command prompt on my-vm-2, install the Nginx web server:
sudo apt-get install nginx-light -y
Use the nano text editor to add a custom message to the home page of the web server:
sudo nano /var/www/html/index.nginx-debian.html
Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR\_NAME with your name
Hi from YOUR\_NAME
use Ctrl+O and Ctrl+X to save and exit
Confirm that the web server is serving your new page. At the command prompt on my-vm-2, execute this command:
curl <http://localhost/>

exit
To confirm that my-vm-2 can reach the web server on my-vm-2, at the command prompt on my-vm-2, execute this command:
curl <http://my-vm-2/>
