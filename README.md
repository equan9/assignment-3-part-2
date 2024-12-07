# Webgen Server Tutorial 
This tutorial will walk through the steps for setting up a web server with a file server and a load balancer. 

## Project Parts 
- Two DigitalOcean droplets running Arch Linux
- Nginx server to serve files and generate index pages
- A load balancer to distribute traffic
- A file server setup to allow downloading of test files

## Project Prerequisites
- The starter code that contains a script to generate an index.html file in the file server. This HTML file will contain the default web content that is displayed when you access your server's IP address. It will link to the directory that contains the test files. The starter code needs to be cloned into your servers
  
## Setup Instructions

### 1. Set Up Two DigitalOcean Droplets (servers)
1. Create two DigitalOcean droplets running Arch Linux.
2. Assign the "web" tag to both droplets.
3. Install Nginx Git Nano (text editor) and Tree on both droplets. 
   ```bash
   sudo pacman -S nginx git nano tree
   # (You may need to update your system first)
   sudo pacman -Syu 
4. Open the Nginx configuration file.
   ```bash
   sudo nano /etc/nginx/nginx.conf
5. Add the location /documents/ block to configure Nginx. This new location block makes it so that users can see and download files from the servers.
   ```bash
   location /documents {
        root /var/lib/webgen;
        autoindex on;
    }
6. Check if there are any issues with the file content.
   ```bash
   sudo nginx -t
7. Start the Nginx service/enable it.
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
8. Check that Nginx has been configured through each server's IP address.

### 2. Set up the File Server
1. Create the directories "/var/lib/webgen/bin", "/var/lib/webgen/documents" and "/var/lib/webgen/HTML" in each server.
   ```bash
   sudo mkdir -p /var/lib/webgen/bin /var/lib/webgen/documents/ /var/lib/webgen/HTML
2. Clone the starter code repository.
   ```bash
   git clone https://git.sr.ht/~nathan_climbs/2420-as3-p2-start
3. Change to the starter code directory.
   ```bash
   cd 2420-as3-p2-start
4. Copy the generate_index script to the appropriate directory "/var/lib/webgen/bin". This will isolate the script from the rest of the files.
   ```bash
   sudo cp generate_index /var/lib/webgen/bin
5. Set execute permissions for the script so that it can run.
   ```bash
   sudo chmod +x /var/lib/webgen/bin/generate_index
6. Change to the bin directory to run the generate_index script. 
   ```bash
   sudo /var/lib/webgen/bin/generate_index
6. Check if it exists in the correct directory. 
7. Next, create test files in the /documents directory, such as "file-one" and "file-two". Check if the files exist in the correct directory. We can download these files later to see if the file server is working correctly.
   ```bash
   echo "file one random content" | sudo tee /var/lib/webgen/documents/file-one
   echo "file two random content" | sudo tee /var/lib/webgen/documents/file-two
8. Verify the tree structure to ensure all the files are in the right place.
9. Create a system user (webgen). It's best to create a system user for web servers so we can limit the permissions and keep all the files secure. 
   ```bash
   sudo useradd -r -s /bin/false webgen
10. Verify that the user has been created successfully.
    ```bash
    getent passwd webgen
11. Change ownership of the directories and files of the server to the webgen system user. 
   ```bash
   sudo chown -R webgen:webgen /var/lib/webgen

## 3. Set up the Load Balancer
A load balancer helps distribute traffic between the servers to make sure the server content is reliably available. If one server is down, the traffic will be redirected to another server so that visitors can still access the same content. 

1. Set up a DigitalOcean load balancer
2. Use the "web" tag to find the created Droplets from earlier. 

## 4. Test the Set-Up
1. Navigate to each server's IP address to view the index.html file.
2. Navigate to each server's IP address/documents directory to view the test files.
3. Navigate to the load balancer's public IP address to check that it can be accessed.




  
