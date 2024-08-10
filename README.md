# nginx-nexus-rhel-setup
# NGINX as SSL Termination for Nexus on RHEL 

repository provides a complete guide for installing and configuring NGINX on Red Hat Enterprise Linux (RHEL) , with a focus on setting up NGINX as an SSL terminator for Nexus Repository Manager. The guide ensures that Nexus is accessible securely over HTTPS only, with detailed instructions covering:
NGINX Installation: Step-by-step process for installing NGINX on RHEL.
SSL Termination: Configuring NGINX to handle SSL traffic, including certificate setup and secure protocol configurations.
Nexus Reverse Proxy: Setting up NGINX as a reverse proxy for Nexus, ensuring all traffic to Nexus is routed through NGINX.
HTTPS Enforcement: Ensuring Nexus is only accessible over HTTPS, with automatic redirection from HTTP.
Nexus Configuration: Adjusting Nexus settings to work seamlessly with NGINX as the reverse proxy.
Firewall Configuration: Setting up the firewall to allow only HTTPS traffic, enhancing security.
Troubleshooting and Tips: Practical advice and common solutions for any issues encountered during setup.
This guide is ideal for system administrators and DevOps professionals looking to securely deploy Nexus on RHEL using NGINX as an SSL termination point.
