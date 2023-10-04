# Deploying HA Infrastructure

This project focus on monitoring and managing infrastructure with high availability. The first step will be to deploy infrastructure to run Prometheus and Grafana, two popular monitoring tools. Once the infrastructure is in place, we will use it to create an SLO/SLI dashboard, which will provide visibility into the performance of an a business application.

Next, we modify existing infrastructure templates and deploy a highly-available infrastructure to AWS in multiple zones using Terraform. Terraform is an infrastructure as code tool that allows you to define your infrastructure in a human-readable configuration file. This makes it easy to deploy and manage your infrastructure in a consistent and repeatable way.

In addition to deploying the infrastructure, we also deploy a RDS database cluster with a replica in an aditional zone. This will ensure that the database is highly available and can continue to operate even if the first zone goes down.