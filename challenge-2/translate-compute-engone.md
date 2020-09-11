
# Google Cloud Fundamentals: Getting Started with Compute Engine
## Objectives
In this lab, you will learn how to perform the following tasks:

- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

- Create a Compute Engine virtual machine using the gcloud command-line interface.

- Connect between the two instances.

 
 ### Task 1: Create a virtual machine using the GCP Console
 Create vm instanse 
 ```
 gcloud compute instances create my-vm-1 \
 --machine-type"n1-standard-1" \
 --image-project "debian-cloud" \
 --image"debian-9-stretch-v20190214"\
 --subnet "default" --tags "http"
 ```
 Create firewall rule
	```
	gcloud compute firewall-rules create allow-http \
	--action= ALLOW \
	--destination= INGRESS \
	--rules=http:80 \
	--target-tags= http
	```


 ### Task 2: Create a virtual machine using the gcloud command line
 1. List zones associated with us-central1 
	 ```gcloud compute zones list | grep us-central1
	 ```

 2. Set zone to anything from the list other that default.
	 ```
	 $ gcloud config set compute/zone us-central1-c
	 ```
3. To create a VM instance called my-vm-2 in that zone, execute this command
	
	
	```gcloud compute instances create "my-vm-2" \
	--machine-type "n1-standard-1" \
	--image-project "debian-cloud" \
	--image "debian-9-stretch-v20190213" \
	--subnet "default"
	```
	
### Task 3: Connect between VM instances
1. Connect to my-vm-2 via ssh
	```
	gcloud compute ssh my-vm-2
	```
2. Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
	```
	ping -c 8 my-vm-1
	```
3. Use the ssh command to open a command prompt on my-vm-1:
	```
	ssh my-vm-1
	```
	If you are prompted about whether you want to continue connecting to a host with unknown authenticity, enter yes to confirm that you do.

4. At the command prompt on my-vm-1, install the Nginx web server:
	```
	$ sudo apt-get install nginx-light -y
	```
5. Use the nano text editor to add a custom message to the home page of the web server:
	```
	sudo nano /var/www/html/index.nginx-debian.html
	```
6. Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
	```
	Hi from Mathapelo
	```
7. Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.

8. Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
	```
	curl http://localhost/
	```
	The response will be the HTML source of the web server's home page, including your line of custom text.

9. To exit the command prompt on my-vm-1, execute this command:
	```
	exit
	```
	You will return to the command prompt on my-vm-2
10. To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
	```
	curl http://my-vm-1/
	```
	The response will be the HTML source of the web server's home page, including your line of custom text.

11. Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text.
