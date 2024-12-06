# Webgen Server Tutorial 
This tutorial will walk through the steps for setting up a web server with a file server and a load balancer. 

## Project Parts 
- Two DigitalOcean droplets running Arch Linux
- Nginx server to serve files and generate index pages
- A load balancer to distribute traffic
- A file server setup to allow downloading of test files

## Project Prerequisites
- A new Github repository with a READ.me file.
- The starter code that contains a script to generate an index.html file in the file server. This HTML file will contain the default web content that is displayed when you access your server's IP     address. It will link to the directory that contains the test files. The starter code needs to be cloned into your repository. 
- 

## Setup Instructions

### 1. Set Up Two DigitalOcean Droplets (servers)

1. Create two DigitalOcean droplets running Arch Linux.
2. Assign the "web" tag to both droplets.
3. Install Nginx and Git on both droplets.
4. Clone the repository onto both droplets using SSH.
5. Configure Nginx on Both Servers.
6. Open the Nginx configuration file.
7. Add the location /documents/ block to the configuration.
8. Restart Nginx.
9. Check that Nginx has been configured through each server's IP address.

### 2. Set up the File Server

1. Create the directories "/var/lib/webgen/bin", "/var/lib/webgen/documents" and "/var/lib/webgen/HTML" in each server. "/var/lib/webgen/HTML" is where the updated script will generate an HTML document.  
2. Since we are using a system user, we need to change the permissions for the user so they can write in the directories.
3. Copy the generate_index script to the appropriate directory "/var/lib/webgen/bin"
4. Set execute permissions for the script so that it can run.
5. Generate the index.html file. Check if it exists in the correct directory. 
6. Next, create test files in the /documents directory, such as "file-one" and "file-two". Check if the files exist in the correct directory. We can download these files later to see if the file server is working correctly.

## 3. Set up the Load Balancer
1. Set up a DigitalOcean load balancer
2. Use the "web" tag to find the created Droplets from earlier. 

## 4. Test the Set Up
1. Navigate to each server's IP address to view the index.html file.
2. Navigate to each server's IP address/documents directory to view the test files.
3. Navigate to the load balancer's public IP address to check that it can be accessed.




  
