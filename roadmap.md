# 🛠️ DevOps Pathway (Part 1)  🛠️ 

Note: Start here if you are new to DevOps & IT

**Level 1 (FUNDAMENTALS)**

**- Linux**
- Basics of Linux Command Line
- Navigating directories & manipulation (ls, cd, mv, cp, mkdir, touch, echo)
- Process monitoring (ps, top, lsof)
- Package management (apt, yum, dnf)
- User and group management (useradd, usermod)
- User/group permissions (chmod, chown, chgrp)
- Text editors: Vim, nano (move around vim and how to exit vim)
- Networking & Troubleshooting tools (netstat, ps aux, ping, dig, traceroute, nslookup)
- Text processing (grep, awk, sed)
- Setup your own local Linux VM using VirtualBox/Vagrant or in the cloud

**- Git fundamentals**
- Basics (cloning, ssh setups etc)
- Commits
- Branching
- Merging
- Pull/Merge Requests

 **- Networking fundamentals**  🌐 
- OSI Model (Layer 1 to 7)
- IP/TCP/UDP
- DNS
- Firewalls (stateless/stateful)
- CIDR/Subnetting
- HTTP/HTTPS/SSL/TTL
- Forward vs Reverse Proxy (Load Balancers)

 **- Cloud I (AWS or Azure or GCP)**
- IaaS/PaaS/SaaS
- Cloud vs on-prem
- Cloud benefits, security etc
- Networking (AWS VPC, Azure VN & more)
- Compute services (AWS EC2/Azure VMs etc)
- Storage services (AWS EFS/EBS/S3, Azure Files/Azure Blobs)
- Database services (AWS RDS/Azure SQL, AWS Aurora/Azure SQL Serverless, AWS DynamoDB/Azure Cosmos)
- Security (IAM, Secrets Manager etc)
- Containers (AWS ECS/EKS, Azure AKS)
- CICD (AWS Code Deploy/Commit/Pipeline/Build, Azure DevOps)
- Monitoring (AWS CloudWatch, CloudTrail, Azure Monitor)
- IaC (AWS CloudFormation, ARM, Bicep)
- Serverless (AWS Lambda, Azure Functions)
- IoT/ML

**Level 2 (Infrastructure & Containers)**

**- Cloud II: AWS or Azure**

  - Containers (AWS ECS/EKS, Azure AKS)
  - CICD (AWS Code Deploy/Commit/Pipeline/Build, Azure DevOps)
  - Monitoring (AWS CloudWatch, CloudTrail, Azure Monitor)
  - IaC (AWS CloudFormation, ARM, Bicep) Serverless (AWS Lambda, Azure Functions)
  - IoT/ML

**- Terraform - Recommended <:terraform:939199273298432122-**
- IaC basics
- Terraform state
- Terraform backend & state locking
- Vars and modules
- Using TF with common providers
- Terraform workflow (tf init, plan, apply, fmt, validate, destroy, import, refresh)
- Create your own Terraform module and use it in different environments (prod, staging, dev etc) - Project

**- Containers (Docker and Kubernetes) - Recommended**
- What are containers? Compared to VMs
- Images, writing Dockerfiles
- Volumes
- Multiple containers (docker compose)
- Advanced Docker (security in Dockerfiles - image size, user perms,  less layers etc)

- What is K8s? How is it different to Containers? 
- Understand K8s architecture and components
- Understanding K8s resources (pods, deployments, services, network policy, rbac, namespaces, PVCs, ingress etc)
- K8s in the Cloud (EKS/AKS/GKE)

**- CI/CD (GitHub Actions, Jenkins, GitLab, Azure DevOps) - Recommended**
- What is CICD? How CICD fits into DevOps?
- Using CICD to automate processes
- Writing pipeline YAML/Jenkins files etc
- Using CICD for building, testing, deploying apps
- GitHub Actions
- GitLab CICD

**Level 3 (Scripting & Coding)**

**- Python/Golang**
- Programming basics
- Data types
- Vars
- Control flow (if/else)
- Functions
- Common libraries
- Projects
- Contribute to open-source projects written in the language you are learning.

# 🛠️ DevOps Roadmap 🛠️ (Part 2)

**Important note: Only move to this once you have completed levels 1-3**

**Level 4 (Monitoring & Infra Management)**

**- Helm (pre-req: Containers) - Optional** 📦
- What is Helm? Link to K8s? 
- Managing deployments and K8s resources using Helm
- Common helm commands (helm install , upgrade, rollback, repo add/update/list, list, env, plugin, create, lint, pull)
- Creating Helm charts and customising it
- Look into Kustomize (alternative for Helm)

**- Ansible  - Optional**
- What is Config mgmt? Diff types? How is it different to Terraform/IaC?
- Creating playbooks
- Creating roles
- Using Ansible galaxy
- Using env vars
- Automating server update/config with Ansible
- Integration with other providers

**- Monitoring tools (Prometheus, ELK, New Relic, DataDog)**
- How monitoring connects to all these?
- When to use it?
- Setting up alerts and monitoring initially
- Pager Duty and alarms
- Responding to alerts and alarms
- On-call and how it works
- Post-mortems and documentation etc

**- SRE**
- SLI/SLO/SLAs
- Post-mortems and documentation
- Incident response & incident management
- Runbooks
- Reducing TOIL
- Error budgets, service monitoring and alerting
- Chaos Engineering
- SRE at Google

**Level 5 (Advanced DevOps, Platform Engineering)**

**- Testing Infrastructure & Integrations  🏗️ 🧪**

- Terratest (Testing Terraform modules)
- Terragrunt (Wrapper, Dependency Management & Reusability))
- Ansible molecule testing framework (Testing Ansible roles)

**Learn more about Cloud Native Technologies 🌩️**

- Look into CNCF projects (graduated + incubating)
- Istio, Linkerd
- K8s operators
- Calico, Cilium

**Security 🛡️**

- Automated security testing
- Vulnerability testing
- Static scanning (Checkov, Trivy)
- Security monitoring

**Advanced CI/CD & GitOps 🔄**
- GitOps: ArgoCD, FluxCD

**Serverless ☁️**
- AWS Lambdas
- Azure Functions
- GCP Cloud Functions
- OpenFaaS

**Chaos Engineering ⚡️**

- Chaos Monkey
- Gremlin
- Chaos Toolkit

**Cloud Native Networking 🌩️ 🌐**

- Service Mesh
- Ingress controllers (Nginx ingress, Traefik)
- Global load balancing

**Advanced Monitoring**
- Distributed Tracing (Jaeger, Zpikin)
- Advanced log management: ELK (Elasticsearch, Logstash, Kibana), Splunk, Graylog
- Time Series Databases: InfluxDB, Prometheus
- APM (Application Performance Monitoring): New Relic, Dynatrace, AppDynamics

**System Design 🖋️🏛️**

- Scaling, Availability
- Forward/Reverse proxies, load balancing
- CDN/Caching
- Messaging Queues
- Databases & DB architecture (replication, sharding, indexing etc)
- Pub/Sub, Event-driven architecture
- API Gateways

Level 5 is endless and I can keep going! Tech is an ever-evolving field. You are not expected to know everything but you are expected to be ready to learn new things every day.

Remember to keep exploring emerging tools and technologies as the DevOps landscape continues to evolve.
