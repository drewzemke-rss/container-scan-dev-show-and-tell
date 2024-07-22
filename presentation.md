---
author: Alex and Drew,
date: July 29, 2024
paging: Slide %d / %d
<!-- theme: ./themes/catppuccin-mocha.json -->
---

# Container Scanning and You
RSS Dev Show & Tell 

---

## What?

  - what is container scanning?
    - scans your docker server image
    - uploads results to a panel in Github
    - we use an open-source tool called `trivy`
  - the goal is to catch vulnerabilities introduced by
    - `pnpm`
    - the base docker image
    - other non-TypeScript dependencies that you use in your docker image

---

## Why?

  - we're no longer using `snyk`; its functionality has been replaced by:
    - Dependabot
    - GH Advanced Security
    - this container scan action 
  - centralized reporting of security vulnerabilities (*show browser*)
  - benefits for our Ops team

---

## How?

  - create an action in your repo
  - including in pipeline
  - how to diagnose vulnerabilities

- mention `rss-actions` at end, before breakout groups. like, check these out!
  - smoke test 
  - retag and deploy
  - container scan (obv)

- breakout groups (with teams? ask Aya)

