---
title: v0.9.53 Armory Agent Clouddriver Plugin (2022-05-11)
toc_hide: true
version: 00.09.53

---

##Fixes

* Fixes the missing `serverGroups` info for agent accounts when calling `GET /applications/{app}/clusters/{agentAccount}/{deployment}`.

**Note:** the `app`, `agentAccount` and `deployment` path variables are case-sensitive.