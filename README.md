# WordpressProject

# Automated Deployment of WordPress with Nginx, LEMP Stack, and GitHub Actions

This repository contains scripts and configuration files to automate the deployment of a WordPress website using Nginx as the web server, LEMP stack (Linux, Nginx, MySQL, PHP), and GitHub Actions for CI/CD. The deployment includes setting up SSL/TLS certificates using Let's Encrypt for secure communication and optimizing the Nginx server configuration for better website performance.

## Prerequisites

- Ubuntu 22.04 AWS EC2 instance
- GitHub repository containing WordPress source code
- Domain name pointing to your server's IP address

## Deployment Steps

1. **Set Up the EC2 Instance**

   - Launch an Ubuntu 22.04 EC2 instance on AWS.
   - SSH into the instance using your key pair.

2. **Install Dependencies**

   - Install required packages: `sudo apt update && sudo apt install nginx mysql-server php-fpm php-mysql certbot python3-certbot-nginx`.

3. **Configure Nginx**

   - Copy the Nginx configuration files from this repository to `/etc/nginx/sites-available/` and create symbolic links in `/etc/nginx/sites-enabled/`.
   - Update the configuration files with your domain name and project-specific details.
   - Test and reload Nginx configuration: `sudo nginx -t && sudo systemctl reload nginx`.

4. **Install and Configure MySQL**

   - Run MySQL secure installation: `sudo mysql_secure_installation`.
   - Create a new MySQL database and user for WordPress.

5. **Clone Your GitHub Repository**

   - Clone your WordPress project repository onto the server.

6. **Configure GitHub Actions**

   - In your repository, create a `.github/workflows` directory.
   - Add a GitHub Actions workflow YAML file (e.g., `deploy.yml`) with the necessary steps:
     - Install dependencies (`apt-get`, PHP packages, etc.).
     - Build the project (if needed).
     - Securely transfer files to the server using SCP or other methods.

7. **SSL/TLS Certificate Setup**

   - Run Certbot to obtain Let's Encrypt SSL/TLS certificates: `sudo certbot --nginx`.
   - Configure Nginx to use the obtained certificates.

8. **Optimize Nginx Configuration**

   - Update Nginx configuration to include caching, gzip compression, and other performance-enhancing settings.
   - Test and reload Nginx configuration: `sudo nginx -t && sudo systemctl reload nginx`.

9. **Run the GitHub Actions Workflow**

   - Push a change to your repository to trigger the GitHub Actions workflow.
   - The workflow should execute steps to install dependencies, build the project, and transfer files to the server.

10. **Access Your Website**

    - Visit your domain name using a web browser. You should see your WordPress website served securely over HTTPS.

## Maintenance

- Regularly update your server, Nginx, PHP, and WordPress for security and performance improvements.
- Monitor your server's resource usage and website performance.

## Troubleshooting

- If you encounter issues, check the Nginx error logs: `sudo tail -f /var/log/nginx/error.log`.


