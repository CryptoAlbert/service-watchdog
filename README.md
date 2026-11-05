# Service watchdog

External HTTPS monitoring using standard GitHub-hosted runners. This repository contains generic monitoring code only. Target address, authentication and alert delivery credentials are repository Actions secrets. No application source, customer data, private wording or credentials are published here.

Checks run every five minutes. GitHub schedules may be delayed; this is not a guaranteed five-minute SLA. The monitor refreshes a generic monthly activity marker because GitHub can disable scheduled workflows on inactive public repositories after 60 days. The owner should still monitor workflow activity and move to a dedicated uptime service when stronger guarantees are needed.

Required secrets: SERVICE_URL and HEALTH_KEY. GitHub notifications are delivered by assigning incident issues, created by github-actions[bot], to the repository owner. Email delivery follows the owner’s GitHub notification preferences. Telegram is optional: configure ALERT_BOT_TOKEN and ALERT_RECIPIENTS (JSON list) only after selecting actual operational recipients. Configure only trusted maintainers. Workflows do not run on pull requests and use no third-party Actions. Generic incident state is stored as repository issues; customer addresses and diagnostics are never included in issue bodies or public logs.

Manual test-alert dispatch sends a clearly labelled test message without stopping the monitored service. Alerting happens when an outage starts and again when it recovers; repeated checks during an open incident do not send duplicate alerts.
