---
SPDX-License-Identifier: MIT
path: "/tutorials/setting-up-a-vps-with-hetzner-cloud-and-coolify-for-n8n-deployment"
slug: "setting-up-a-vps-with-hetzner-cloud-and-coolify-for-n8n-deployment"
title: "Setting Up a VPS with Hetzner Cloud and Coolify for N8N Deployment"
short_description: "Learn to set up a VPS on Hetzner and deploy N8N AI version via Coolify with this easy step-by-step guide."
...
---

Discover how to efficiently set up a virtual private server (VPS) using Hetzner Cloud and deploy N8N using Coolify, an intuitive GUI Docker manager. This guide provides step-by-step instructions to streamline your setup process.

![Hetzner Cloud](https://files.notice.studio/workspaces/8c8c2caf-fbf0-4d85-bcb7-8fb67110ece6/b5fefccf-a4cc-4614-a954-1ba67a8f2221.png)

## Step 1: Order a VPS from Hetzner Cloud

- Begin by ordering a VPS, specifically the **CAX11** model, from Hetzner Cloud. Utilize this [referral link](https://swiy.co/vps) to enjoy a 5-month free VPS offer. The average monthly cost post-offer is approximately $3.6.
  ![Hetzner VPS](https://cdn.statically.io/gh/ARHAEEM/blog/assets/17049677840001b1ado.png)

## Step 2: Select Your Server OS

- Choose **Docker CE** as your server operating system, which can be found in the APPS section.
  ![Docker CE](https://cdn.statically.io/gh/ARHAEEM/blog/assets/1704963901000ce1hwu.png)

## Step 3: Install Coolify

- Once your server is ready, access the console and execute the following command:
  ```BASH
  curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash
  ```
  After the installation, a dashboard URL like `http://xx.xx.xx.xx:8000` will be displayed. Access this URL to set up your Coolify account.
  
## Step 4: Create Database Containers

- Effortlessly create Postgres & Redis Containers. Coolify manages the entire setup, so no additional configuration is necessary.
  ![Database Containers](https://cdn.statically.io/gh/ARHAEEM/blog/assets/1704964301000m1hmn5.png)
  **Note:** Ensure your databases remain private and internal. Do not make them public.

## Step 5: Configure N8N Application

- Add a new resource and select an application based on **Docker Compose**.
  ![N8N Application](https://cdn.statically.io/gh/ARHAEEM/blog/assets/1704964638000gfw54v.png)
- Insert the following Docker Compose configuration.
   ```YAML
  services:
  n8n:
    image: 'docker.n8n.io/n8nio/n8n:ai-beta'
    environment:
      - SERVICE_FQDN_N8N
      - 'N8N_EDITOR_BASE_URL=${SERVICE_FQDN_N8N}'
      - 'WEBHOOK_URL=${SERVICE_FQDN_N8N}'
      - 'N8N_HOST=${SERVICE_DOMAIN_N8N}'
      - 'GENERIC_TIMEZONE="Europe/Berlin"'
      - 'TZ="Europe/Berlin"'
      - 'DB_POSTGRESDB_DATABASE=${DB_POSTGRESDB_DATABASE}'
      - 'DB_POSTGRESDB_HOST=${DB_POSTGRESDB_HOST}'
      - 'DB_POSTGRESDB_PASSWORD=${DB_POSTGRESDB_PASSWORD}'
      - 'DB_POSTGRESDB_PORT=${DB_POSTGRESDB_PORT}'
      - 'DB_POSTGRESDB_SCHEMA=${DB_POSTGRESDB_SCHEMA}'
      - 'DB_POSTGRESDB_USER=${DB_POSTGRESDB_USER}'
      - 'DB_TYPE=${DB_TYPE}'
      - 'EXECUTIONS_MODE=${EXECUTIONS_MODE}'
      - 'N8N_LOG_LEVEL=${N8N_LOG_LEVEL}'
      - 'N8N_METRICS=${N8N_METRICS}'
      - 'QUEUE_BULL_PREFIX=${QUEUE_BULL_PREFIX}'
      - 'QUEUE_BULL_REDIS_DB=${QUEUE_BULL_REDIS_DB}'
      - 'QUEUE_BULL_REDIS_HOST=${QUEUE_BULL_REDIS_HOST}'
      - 'QUEUE_BULL_REDIS_PASSWORD=${QUEUE_BULL_REDIS_PASSWORD}'
      - 'QUEUE_BULL_REDIS_PORT=${QUEUE_BULL_REDIS_PORT}'
      - 'N8N_DIAGNOSTICS_ENABLED=${N8N_DIAGNOSTICS_ENABLED}'
      - 'N8N_VERSION_NOTIFICATIONS_ENABLED=${N8N_VERSION_NOTIFICATIONS_ENABLED}'
      - 'N8N_TEMPLATES_ENABLED=${N8N_TEMPLATES_ENABLED}'
      - 'EXTERNAL_FRONTEND_HOOKS_URLS=${EXTERNAL_FRONTEND_HOOKS_URLS}'
      - 'N8N_DIAGNOSTICS_CONFIG_FRONTEND=${N8N_DIAGNOSTICS_CONFIG_FRONTEND}'
      - 'N8N_DIAGNOSTICS_CONFIG_BACKEND=${N8N_DIAGNOSTICS_CONFIG_BACKEND}'
      - 'N8N_ONBOARDING_FLOW_DISABLED=${N8N_ONBOARDING_FLOW_DISABLED}'
    volumes:
      - 'n8n-data:/home/node/'```

## Step 6: Set Environment Variables

- After creating the container, navigate to the **Environment Variables** section and enable **Developer Mode** to view and edit all configurable options.
  ![Environment Variables](https://cdn.statically.io/gh/ARHAEEM/blog/assets/1704965377000qtaxfj.png)
- Utilize the URLs copied from the Postgres & Redis setup to configure the respective environment variables.

![gh](https://cdn.statically.io/gh/ARHAEEM/blog/assets/1704965971000ximppt.png)
![gh](https://cdn.statically.io/gh/ARHAEEM/blog/assets/1704967157000cdm9h4.png)

final Env config will look like this example:
```YAML
DB_POSTGRESDB_DATABASE=postgres
DB_POSTGRESDB_HOST=k4o4wwk
DB_POSTGRESDB_PASSWORD=Ka36bNFBdHUtmvs3ZPKk2iWx8N
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_SCHEMA=public
DB_POSTGRESDB_USER=postgres
DB_TYPE=postgresdb
EXECUTIONS_MODE=queue
EXTERNAL_FRONTEND_HOOKS_URLS=
N8N_DIAGNOSTICS_CONFIG_BACKEND=false
N8N_DIAGNOSTICS_CONFIG_FRONTEND=false
N8N_DIAGNOSTICS_ENABLED=false
N8N_LOG_LEVEL=verbose
N8N_METRICS=false
N8N_ONBOARDING_FLOW_DISABLED=true
N8N_TEMPLATES_ENABLED=true
N8N_VERSION_NOTIFICATIONS_ENABLED=true
QUEUE_BULL_PREFIX=N8N_
QUEUE_BULL_REDIS_DB=0
QUEUE_BULL_REDIS_HOST=xsksg8s
QUEUE_BULL_REDIS_PASSWORD=Si8oa82GpHLS44lw8Ssm
QUEUE_BULL_REDIS_PORT=6379
SERVICE_DOMAIN_N8N=rmQirts0xAxkgDAd
SERVICE_FQDN_N8N=http://n8n-n4cw2c.65.19.17.197.sslip.io
```
## Final Steps: Deploy and Enjoy N8N

- Once you have filled in your configurations, click **Save** and then **Deploy**.
  ![Deploy N8N](https://cdn.statically.io/gh/ARHAEEM/blog/assets/1704967523000tlea6n.png)
- Upon successful deployment, you can start using N8N. If it's your first time, you'll be directed to the registration page to set up an admin account.

## Additional Configurations and Tips

- This tutorial does not cover setting up a Cloudflare account, CNAME, Firewall, Webhooks, or Hetzner Firewall rules. These are essential for a secure and fully functional setup.
- You can rescale your server in the near future once your usage excused.
- To support N8N Project, you can also use their [cloud version](https://n8n.io/pricing/). which is hassle free and everything managed by them.
- If you need any help with N8N fixing and building workflows, use our GPT model made for N8N Assistance [here](https://swiy.co/n8n).

For more detailed information on environment variables and advanced configurations, refer to the [N8N Documentation](https://docs.n8n.io/hosting/environment-variables/environment-variables/).

---

**Keywords for SEO**: VPS, Hetzner Cloud, Docker, Coolify, N8N, Cloud Hosting, Virtual Private Server, Docker CE, Database Containers, GUI Docker Manager, Environment Variables, Deployment, Cloudflare, Firewall, Webhooks
