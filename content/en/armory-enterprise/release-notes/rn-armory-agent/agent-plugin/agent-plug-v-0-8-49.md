---
title: v0.8.49 Armory Agent Clouddriver Plugin (2022-03-04)
toc_hide: true
version: 00.08.49

---

## Changes

Update the account that creates the release versions. This change does not impact end users.

## Known Issues

* The plugin makes a request to fiat `/sync/roles` endpoint every time an agent connects or accounts are deleted. This can become an issue when having a large number of agents connected to a clouddriver pod that is restarted.
