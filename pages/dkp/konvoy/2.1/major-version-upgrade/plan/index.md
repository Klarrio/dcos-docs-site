---
layout: layout.pug
navigationTitle: Plan Your Upgrade
title: Plan Your Upgrade
menuWeight: 30
excerpt: Planning for the preparation work, processes to complete, and changes before beginning the major version upgrade
beta: true
enterprise: false
---

Because a major version upgrade can take significant time, it is important to plan the effort carefully.

The following steps represent preparation work that you need to complete before you can begin the major version upgrade:

1.  Upgrade clusters to the specified OS version.

1.  Upgrade Konvoy sequentially to at least Konvoy v1.8.3, which includes the required version of Kubernetes, 1.20.6.

1.  **REQUIRED** Back up the current configuration, using Velero.

1.  **Optional** Create a diagnostics bundle. This is a best practice and will help D2iQ assist in troubleshooting.

The major version upgrade includes [upgrades to the platform applications](/dkp/kommander/2.1/major-upgrade/upgrade-clusters/migrate-platform-apps), formerly known as addons, provided with DKP.
