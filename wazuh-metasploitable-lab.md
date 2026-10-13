---
title: "Wazuh + Kali + Metasploitable 3 SOC Lab"
layout: single
permalink: /wazuh-metasploitable-lab/
author_profile: true
classes: wide
---

<div class="project-banner"><span class="status status-progress">In progress</span><p>A small, isolated lab for learning how security events are generated, collected, investigated, and documented.</p><div class="hero-tags"><span>Wazuh</span><span>Kali Linux</span><span>Metasploitable 3</span><span>VirtualBox</span></div></div>

## Objective

Build familiarity with the SOC workflow by generating controlled activity against a deliberately vulnerable lab target, reviewing the resulting Wazuh events and alerts, and documenting what the evidence does—and does not—show.

## Lab architecture

<div class="architecture-diagram"><div class="arch-node arch-kali"><span>01</span><strong>Kali Linux</strong><small>Testing workstation</small><code>Nmap · Hydra</code></div><div class="arch-arrow">⇄<small>isolated lab network</small></div><div class="arch-node arch-target"><span>02</span><strong>Metasploitable 3</strong><small>Authorized lab target</small><code>Linux · endpoint logs</code></div><div class="arch-arrow arch-up">↑<small>agent telemetry, where configured</small></div><div class="arch-node arch-wazuh"><span>03</span><strong>Wazuh</strong><small>Monitoring &amp; alert review</small><code>Events · rules · alerts</code></div></div>

> Keep Metasploitable 3 isolated from the public Internet and unrelated devices. Use Hydra only against accounts and services in this lab that you own or are explicitly authorized to test. Avoid high-volume attempts; stop when you have enough evidence to investigate.

## Current progress
- [x] Wazuh manager, indexer, and dashboard running.
- [x] Lab network configured and target IP identified.
- [x] Wazuh agent appears in the dashboard and has been brought to a working state.
- [x] Nmap scan generated visible Wazuh results.
- [x] Controlled Hydra test generated visible Wazuh results.
- [ ] Identify the exact rule IDs and descriptions for both tests.
- [ ] Confirm which events originate from endpoint logs versus other data sources.
- [ ] Compare event timestamps with the test timeline.
- [ ] Document findings, limitations, and defensive recommendations.

## Investigation workflow
<div class="process-row"><div><b>01</b><strong>Generate</strong><small>Run a controlled lab test</small></div><div><b>02</b><strong>Observe</strong><small>Find matching events</small></div><div><b>03</b><strong>Correlate</strong><small>Compare time and source</small></div><div><b>04</b><strong>Report</strong><small>Explain evidence and gaps</small></div></div>

## Exercise 1 — Nmap reconnaissance
**Goal:** determine which Wazuh events appeared around the time of a known Nmap scan.

1. Note the Kali IP, target IP, exact scan command, and local time.
2. In Wazuh Threat hunting / Security events, choose a time range that includes the scan.
3. Open a relevant event and record the timestamp, agent, rule ID, description, severity, source/destination fields if present, and full log.
4. Do not conclude that an alert was caused by Nmap solely because it appeared at a similar time. Confirm the source and event details.
5. Record whether the event is a detection of network activity, an endpoint log, or another event type.

### Evidence to add
<div class="evidence-grid"><div class="evidence-placeholder"><span>01</span><strong>Wazuh alert details</strong><small>Replace with your screenshot</small></div><div class="evidence-placeholder"><span>02</span><strong>Nmap output</strong><small>Replace with your terminal capture</small></div></div>

## Exercise 2 — Controlled authentication testing
**Goal:** examine the Wazuh events generated during a small, authorized Hydra test against a lab service.

1. Record the target service and the time of the test.
2. Use only a test account and a small, controlled attempt set on the isolated VM.
3. Review Wazuh alerts for authentication failures, relevant rule descriptions, affected agent, and event details.
4. Check the target's relevant authentication/service logs where available.
5. Separate failed-login evidence from evidence of a successful login. A brute-force tool running does not by itself prove a successful compromise.

### Evidence to add
<div class="evidence-grid"><div class="evidence-placeholder"><span>03</span><strong>Authentication alert</strong><small>Replace with your screenshot</small></div><div class="evidence-placeholder"><span>04</span><strong>Relevant target log</strong><small>Replace with a redacted capture</small></div></div>

## Investigation notes
Use this table when documenting each real event.

| Field | Observation |
|---|---|
| Test | Nmap / controlled authentication test |
| Time window | Add local date and time |
| Source IP | Add if present in the event |
| Target / agent | Add actual agent name and IP |
| Rule ID and description | Copy from Wazuh |
| Severity | Copy the actual rule level |
| Evidence supporting the conclusion | Link screenshot or log excerpt |
| Limitations / unknowns | State what you could not verify |
| Recommended next step | Add a practical defensive action |

## What I am learning

This lab is helping me practice the difference between generating security activity and investigating it. The next step is to validate each alert against its source event, identify gaps in telemetry, and document evidence carefully rather than treating every alert as proof of compromise.

## References
- [Wazuh documentation](https://documentation.wazuh.com/current/)
- [Nmap reference guide](https://nmap.org/book/man.html)
