# HAIL & EPM Deployment Guide

**Authors:** Sagar, Bala  

This document outlines the deployment steps for the HAIL and EPM applications across **UAT, Staging, and Production environments**.

---

## Environments

| Environment | Server | Notes |
|------------|--------|-------|
| Staging (local deployments) | `LDRSRVTS02 - 10.10.10.4` | Local deployments |
| Staging (client deployments) | `LDRVMTSRV04 - 10.14` | Client deployments |
| Both EPM & HAIL | `10.10.10.22` | Handles both applications |

### SSH Access

```bash
ssh frappe@10.10.10.22
# Provide password when prompted
Directory Structure
bash
Copy code
cd hail_epm_staging/frappe-bench
ls
# apps, config, env, logs, patches.txt, Procfile, sites
Apps
Core apps (no changes needed):
erpnext, frappe, hrms, payments

Custom apps (we modify these):
foxerp, foxerp_civic_cloud, foxerp_epm, foxerp_hail

Other apps (used in UAT/Prod only):
foxerp_integration, zatca

Sites
Site	Apps
EPM	foxerp, foxerp_civic_cloud, foxerp_epm
HAIL	foxerp, foxerp_civic_cloud, foxerp_hail

bash
Copy code
cd sites
ls
# epmstaging14.foxerp.com   hailstaging.leadergroup.com
Bench Commands
Note: These commands work inside frappe-bench directory.

bash
Copy code
bench --site epmstaging14.foxerp.com list-apps
bench --site hailstaging.leadergroup.com list-apps
Deployment Steps
EPM Deployment
bash
Copy code
cd apps/foxerp
git status
# copy branch name (e.g., staging-ver-14)
git pull upstream staging-ver-14
# provide git username and PAT

cd ../foxerp_epm
git status
git pull upstream staging-ver-14
# provide git username and PAT

cd ../foxerp_civic_cloud
git status
git pull upstream staging-ver-14
# provide git username and PAT
bash
Copy code
# Migrate and restart EPM site
bench --site epmstaging14.foxerp.com migrate
bench --site epmstaging14.foxerp.com clear-cache
bench --site epmstaging14.foxerp.com clear-website-cache
bench build
bench restart
HAIL Deployment
bash
Copy code
cd apps/foxerp_hail
git status
git pull upstream staging
bash
Copy code
# Migrate and restart HAIL site
bench --site hailstaging.leadergroup.com migrate
bench --site hailstaging.leadergroup.com clear-cache
bench --site hailstaging.leadergroup.com clear-website-cache
bench build
bench restart
General Notes
If there is only one site under apps, you can use:

bash
Copy code
bench migrate
Always pull the correct branch (staging-ver-14 for EPM, staging for HAIL) before migration.

Ensure you provide your git username and Personal Access Token (PAT) when prompted.
