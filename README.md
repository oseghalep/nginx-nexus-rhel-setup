# nginx-nexus-rhel-setup
# NGINX as SSL Termination for Nexus on RHEL 

repository provides a complete guide for installing and configuring NGINX on Red Hat Enterprise Linux (RHEL) , with a focus on setting up NGINX as an SSL terminator for Nexus Repository Manager. The guide ensures that Nexus is accessible securely over HTTPS only, with detailed instructions covering:

1. NGINX Installation: Step-by-step process for installing NGINX on RHEL.
2. SSL Termination: Configuring NGINX to handle SSL traffic, including certificate setup and secure protocol configurations.
3. Nexus Reverse Proxy: Setting up NGINX as a reverse proxy for Nexus, ensuring all traffic to Nexus is routed through NGINX.
4. HTTPS Enforcement: Ensuring Nexus is only accessible over HTTPS, with automatic redirection from HTTP.
5. Nexus Configuration: Adjusting Nexus settings to work seamlessly with NGINX as the reverse proxy.
6. Firewall Configuration: Setting up the firewall to allow only HTTPS traffic, enhancing security.
7. Troubleshooting and Tips: Practical advice and common solutions for any issues encountered during setup.
8. This guide is ideal for system administrators and DevOps professionals looking to securely deploy Nexus on RHEL using NGINX as an SSL termination point.

9. # Install NGINX
10. Follow the guide on the repository below to install NGINX before configuring Nexus to use NGINX for SSL traffic Termination
# https://github.com/oseghalep/NGINX-Install-RHEL
