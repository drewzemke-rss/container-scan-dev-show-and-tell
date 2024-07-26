---
author: Alex and Drew,
date: July 29, 2024
paging: Slide %d / %d
<!-- theme: ./themes/catppuccin-mocha.json -->
---

# Container Scanning and You

RSS Dev Show & Tell

---

## What is Container Scanning?

- the goal is to catch vulnerabilities introduced by:
  - the base docker image
  - other non-TypeScript dependencies that you use in your docker image (eg. `pnpm`)
   <br/>
- we created a GitHub action that:
  - scans your docker server image
  - uses an open-source tool called `trivy`
  - uploads results to a panel in Github

---

## Why Container Scan?

- we're no longer using `snyk`; its functionality has been replaced by:
  - Dependabot (TS/JS dependency versions)
  - GH Advanced Security (static security analysis, incl. secret scanning)
  - **this container scan action**
   <br/>
- centralized reporting of security vulnerabilities (*demo*)
   <br/>
- benefits for our Ops/Security folks
  - provides flexibility for auditing containers running in different environments

---

## How Does One Container Scan?

- first, remove `snyk` from your pipeline

### Include Container Scan in Your Pipeline

```yaml
container_scan:
  needs: [server]
  name: Container Security Scan
  runs-on: ubuntu-latest
  steps:
    - name: Container Scan
      uses: risk-and-safety/rss-actions/actions/container-scan@v2
      with:
        image: ghcr.io/risk-and-safety/<APP-NAME>/server:latest
        name: '<APP-NAME>'
        slack-channel-id: '#my-slack-channel'
        slack-bot-token: ${{ secrets.SLACK_BOT_TOKEN }}
        github-docker-password: ${{ secrets.RSS_SVC_GITHUB_DOCKER_PASSWORD }}
        github-actor: ${{ github.actor }}
```

---

## How Does One Container Scan?

### Create a Scheduled Action in Your Repo

```yaml
name: Daily Container Security Scan

on:
  schedule:
    - cron: '0 14 * * *'

jobs:
  container_scan:
    name: Container Security Scan
    runs-on: ubuntu-latest
    steps:
      - name: Container Scan
        uses: risk-and-safety/rss-actions/actions/container-scan@v2
        with:
          image: ghcr.io/risk-and-safety/<APP-NAME>/server:latest
          name: '<APP-NAME>'
          slack-channel-id: '#my-slack-channel'
          slack-bot-token: ${{ secrets.SLACK_BOT_TOKEN }}
          github-docker-password: ${{ secrets.RSS_SVC_GITHUB_DOCKER_PASSWORD }}
          github-actor: ${{ github.actor }}
```

---

## How Does One Container Scan?

### Diagnosing Vulnerabilities

- the most common sources of issues are:
  - your base docker image
  - `pnpm`  
  <br>
- share your issues/solutions in `#developers`!

---

## Breakout Rooms

Go put the container scan in your project(s)!

---

## Conclusion

- Need help? Post in `#developers`
  <br>
- RSS Actions exists and is good. Check these out in the `rss-actions` repo!
  - smoke test
  - retag and deploy
  - container scan
  - ... *more to come* :)
