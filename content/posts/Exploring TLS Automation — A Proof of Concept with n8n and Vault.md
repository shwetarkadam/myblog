+++
title = " Exploring TLS Automation — A Proof of Concept with n8n and Vault"
author = ["Shweta Kadam"]
date = 2025-04-20T21:41:00+05:30
tags = ["learning", "public speaking", "presentation", "journey", "talk","n8n","vault"]
draft = false
+++


## Exploring TLS Cert Automation — A Proof of Concept with n8n and Vault

Managing TLS certificates often means chasing expiry dates, setting reminders, and manually rotating certs—a process that’s fragile and prone to outages. To prove there’s a better way, I built a prototype combining n8n and HashiCorp Vault that demonstrates the power of automation, and had the opportunity to present this work as a talk at Mumbai FOSS 2025.
The Prototype in Action

The workflow I showcased was simple yet powerful:

Monitoring expiry with early alerts

Triggering automatic renewals via Vault’s PKI engine

Deploying renewed certificates without manual steps

Validating results in Vault for full transparency

This wasn’t a slide deck—it was about demonstrating the ability such a system can provide: hands-off certificate lifecycle management, built entirely on open-source tools.

Why n8n + Vault?

n8n brings the flexibility of a visual automation platform—easy to extend, no coding required for most steps.

Vault provides a battle-tested PKI engine with strong security guarantees.

Together, they eliminate vendor lock-in, subscription costs, and opaque “black box” processes.

Beyond the Demo

While I shared this prototype in a lightning talk at Mumbai FOSS 2025, the real takeaway is that any team can replicate it today. Whether managing a handful of certs or rolling this out across multiple environments, the approach scales with your needs.

As a bonus, this same session was also wait-listed for the Open Source Summit India 2025, highlighting the growing interest in practical, open-source security automation.
