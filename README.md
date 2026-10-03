# Custom AWS VPC with EC2 Web Server

A hands-on AWS networking and web server deployment project demonstrating how to build a custom Virtual Private Cloud (VPC), configure public internet connectivity, and host a portfolio webpage on an Amazon Linux EC2 instance using Apache HTTP Server.

## Project Overview

The project involved creating a custom VPC, configuring a public subnet and Internet Gateway, setting up route tables and security groups, and deploying an EC2 instance running Apache HTTP Server. The hosted webpage was tested through the instance's public IPv4 address.

**Project Status:** Successfully configured and tested. The AWS resources were subsequently deleted to avoid ongoing charges, so the original website endpoint is no longer expected to be available.

## Architecture

![AWS VPC and EC2 Web Server Architecture](architecture-diagram.png)

### Traffic Flow

1. A user accesses the website through a web browser.
2. Internet traffic reaches the VPC through the Internet Gateway.
3. The public route table directs internet-bound traffic through the Internet Gateway.
4. The Security Group controls inbound access to the EC2 instance.
5. Apache HTTP Server receives HTTP requests on TCP port `80`.
6. The server returns the hosted portfolio webpage to the browser.

## AWS Configuration

| Resource | Configuration |
|---|---|
| VPC | `my-vpc-project` |
| VPC IPv4 CIDR | `10.0.0.0/16` |
| Public Subnet | `public-subnet` |
| Subnet IPv4 CIDR | `10.0.1.0/24` |
| Internet Gateway | `my-project-igw` |
| Route Table | `public-route-table` |
| Default Internet Route | `0.0.0.0/0` via Internet Gateway |
| Security Group | `web-server-SG` |
| Operating System | Amazon Linux |
| EC2 Instance Type | `t3.micro` |
| Web Server | Apache HTTP Server (`httpd`) |
| HTTP Port | TCP `80` |

## EC2 and Apache Deployment

The EC2 instance was configured to host a static portfolio webpage using Apache HTTP Server.

The following commands were used to install, start, enable, and verify the Apache service on Amazon Linux:

```bash
sudo dnf update -y
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

The website's HTML file was placed in Apache's default document root:

```text
/var/www/html/index.html
```

The Apache service was verified as active, and the server was configured to serve HTTP traffic on port `80`.

## Network Security

The `web-server-SG` Security Group was configured to permit web traffic over TCP port `80` and SSH access over TCP port `22`. The captured Security Group evidence also shows an additional custom TCP rule.

For a production deployment, SSH access should be restricted to trusted IP addresses, and unnecessary inbound rules should be removed.

## Deployment Verification

The website was tested in a browser using the EC2 instance's public IPv4 address. The captured evidence showed the portfolio webpage loading successfully.

This test demonstrated connectivity between the public internet, the configured VPC networking components, the EC2 instance, and the Apache web server.

## Implementation Evidence

### 1. VPC Configuration

![VPC Configuration](screenshots/01-vpc.png)

Documents the custom VPC configuration and its IPv4 network range.

### 2. Internet Gateway

![Internet Gateway](screenshots/02-internet-gateway.png)

Documents the Internet Gateway used to provide internet connectivity for the public network path.

### 3. Public Route Table

![Public Route Table](screenshots/03-route-table.png)

Shows the route table configuration for directing internet-bound traffic through the Internet Gateway.

### 4. Security Group

![Security Group](screenshots/04-security-group.png)

Documents the inbound access rules configured for the EC2 web server.

### 5. EC2 Instance

![EC2 Instance](screenshots/05-ec2-instance.png)

Shows the EC2 instance used to host the portfolio webpage.

### 6. Apache Service

![Apache Running](screenshots/06-apache-running.png)

Provides evidence of the Apache HTTP Server running on the instance.

### 7. Working Website

![Working Website](screenshots/07-working-website.png)

Shows the portfolio webpage successfully served through the EC2 instance's public endpoint during testing.

## AWS Services and Technologies

- **Amazon VPC:** Custom network environment for the web server.
- **Amazon EC2:** Compute instance hosting the portfolio webpage.
- **Internet Gateway:** Internet connectivity for the public subnet.
- **Route Tables:** Routing configuration for internet-bound traffic.
- **Security Groups:** Network-level access control for the EC2 instance.
- **Amazon Linux:** Operating system for the web server.
- **Apache HTTP Server:** Serves the static HTML webpage.
- **HTML:** Content displayed on the website.

## Skills Demonstrated

- Creating and configuring a custom AWS VPC.
- Working with IPv4 CIDR blocks and public subnets.
- Configuring an Internet Gateway and public route table.
- Launching and managing an EC2 instance.
- Configuring Security Group inbound rules.
- Installing and managing Apache on Amazon Linux.
- Hosting and testing a static webpage over HTTP.
- Verifying cloud infrastructure through AWS console evidence.
- Documenting a cloud deployment for a technical portfolio.

## Security Considerations

- Restrict SSH access to trusted source IP addresses.
- Allow only the inbound ports required for the application.
- Avoid exposing credentials, private keys, or sensitive account information in the repository.
- HTTPS/TLS was not demonstrated in the captured deployment and remains a potential improvement.
- Additional production improvements include stronger input validation, monitoring, logging, and secure configuration management.

## Cleanup and Cost Management

After testing and capturing the implementation evidence, the EC2 instance was terminated and the associated networking resources were removed to avoid unnecessary AWS charges.

The original deployment is documented through the source files and screenshots rather than a currently running endpoint. Recreating the environment may incur AWS charges depending on the selected region and resource configuration.

## Future Improvements

- Configure HTTPS using TLS certificates.
- Restrict SSH access to trusted IP addresses.
- Configure DNS and a custom domain.
- Add monitoring and logging for operational visibility.
- Automate infrastructure provisioning using AWS CloudFormation or Terraform.
- Consider Amazon S3 for static website hosting where appropriate.

## Repository Structure

```text
aws-vpc-ec2-web-server/
├── README.md
├── index.html
├── architecture-diagram.png
└── screenshots/
    ├── 01-vpc.png
    ├── 02-internet-gateway.png
    ├── 03-route-table.png
    ├── 04-security-group.png
    ├── 05-ec2-instance.png
    ├── 06-apache-running.png
    └── 07-working-website.png
```

---

**Author:** Mohammed Hashir 

**Project:** Custom AWS VPC with EC2 Web Server
