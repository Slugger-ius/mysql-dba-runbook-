# mysql-dba-runbook-
Operational runbooks and automated daily checks for MySQL: replication, backups, capacity, and performance.

# MySQL DBA Runbook (Daily) + Automated Health Checks

This repository contains a practical **daily DBA runbook for MySQL** and an **automated daily health report** that runs via GitHub Actions (recommended on a self-hosted runner) and reports **OK / WARN / CRIT**.

## What’s inside

- `runbook/DAILY_RUNBOOK.md` — step-by-step daily operational checks (replication, backups, capacity, performance, security)
- `scripts/mysql_daily_health_report.sh` — generates a daily health report and exits with:
  - `0` = OK
  - `1` = WARN
  - `2` = CRIT
- `.github/workflows/mysql-daily-dba-health.yml` — scheduled daily workflow (and manual trigger)

## Quick start

### 1) Clone
```bash
git clone <your-repo-url>
cd mysql-dba-runbook
2) Run the health report locally
chmod +x scripts/mysql_daily_health_report.sh

DB_HOST=127.0.0.1 \
DB_PORT=3306 \
DB_USER=root \
DB_PASSWORD='your_password' \
DB_NAME=mysql \
./scripts/mysql_daily_health_report.sh
3) Configure GitHub Actions (daily runs)
Recommended: self-hosted runner

Run the workflow on a self-hosted Linux runner that can reach your MySQL instance on the private network.

Add GitHub Secrets

Repo → Settings → Secrets and variables → Actions:

Required:

DB_HOST

DB_PORT

DB_USER

DB_PASSWORD

DB_NAME

Optional:

SLACK_WEBHOOK_URL (for Slack notifications)

BACKUP_ROOT (only if the runner can access the backup path locally)

4) Run manually (optional)

Actions → MySQL Daily DBA Health → Run workflow

Notes & Safety

Never commit credentials to the repo. Use GitHub Secrets only.

If you make the repo public, ensure the runbook contains no internal hostnames, IPs, usernames, or company procedures.

Roadmap ideas

Add “top offenders” output (longest transactions, blockers) on WARN/CRIT only

Add PITR/binlog retention checks

Export metrics to Prometheus/Grafana
