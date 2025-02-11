---
layout: layout.pug
navigationTitle: Supported Operating Systems
title: Supported Operating Systems
menuWeight: 40
excerpt: Supported operating systems for Konvoy
beta: false
enterprise: false
---

<!-- vale Microsoft.RangeFormat = NO -->

Konvoy supports the following base Operating Systems.

## Amazon Web Services (AWS)

<!-- vale Vale.Spelling = NO -->
<!-- vale Vale.Terms = NO -->
| Operating System                           | Kernel                      | Default Config | FIPS | Air Gapped | FIPS with Air Gapped | GPU Support <!-- vale Vale.Spelling = YES --> <!-- vale Vale.Terms = YES --> |
|--------------------------------------------|-----------------------------|----------------|------|------------|----------------------|-------------|
| [CentOS 7.9][centos7]                      | 3.10.0-1160.el7.x86_64      | Yes            | Yes  | Yes        | Yes                  | Yes         |
| [RHEL 7.9][rhel_7_9]                       | 3.10.0-1160.el7.x86_64      | Yes            | Yes  | Yes        |                      | Yes         |
| [RHEL 8.2][rhel_8_2]                       | 4.18.0-193.6.3.el8_2.x86_64 | Yes            | Yes  | Yes        | Yes                  |             |
| [RHEL 8.4][rhel_8_4]                       | 4.18.0-193.6.3.el8_4.x86_64 | Yes            | Yes  |            | Yes                  |             |
| [SUSE Linux Enterprise Server 15][sles_15] |                             | Yes            |      |            |                      | Yes         |
| [Ubuntu 18.04 (Bionic Beaver)][ubuntu_18]  |                             | Yes            |      |            |                      |             |
| [Ubuntu 20.04 (Focal Fossa)][ubuntu_20]    |                             | Yes            |      |            |                      | Yes         |
| [Oracle Linux RHCK 7.9][RHCK]              | kernel-3.10.0-1160.el7      | Yes            | Yes  |   Yes      |  Yes                 |             |

## Pre-Provisioned/On Premises

<!-- vale Vale.Spelling = NO -->
<!-- vale Vale.Terms = NO -->
| Operating System         | Kernel | Default Config | FIPS | Air Gapped | GPU Support <!-- vale Vale.Spelling = YES --> <!-- vale Vale.Terms = YES --> |
|--------------------------|--------|----------------|------|------------|-------------|
| [CentOS 7.9][centos7] | 3.10.0-1160.el7.x86_64 |   |      | Yes        |             |
| [Flatcar][flatcar] | 2905.2.1 | | GPU workloads are not currently supported |
| [Oracle Linux RHCK 7.9][RHCK] | kernel-3.10.0-1160.el7 |  Yes |   Yes   |   Yes         |                      |         |

## Azure

<!-- vale Vale.Spelling = NO -->
<!-- vale Vale.Terms = NO -->
| Operating System                        | Kernel | Default Config | FIPS | Air Gapped | GPU Support <!-- vale Vale.Spelling = YES --> <!-- vale Vale.Terms = YES --> |
|-----------------------------------------|--------|----------------|------|------------|-------------|
| [Ubuntu 20.04 (Focal Fossa)][ubuntu_20] |        | Yes            |      |            |             |

[centos7]: https://wiki.centos.org/action/show/Manuals/ReleaseNotes/CentOS7.2003
[centos8]: https://wiki.centos.org/action/show/Manuals/ReleaseNotes/CentOS8.2004
<!--- [debian_9]: https://www.debian.org/releases/stretch/releasenotes
[debian_10]: https://www.debian.org/releases/buster/releasenotes --->
[flatcar]: https://www.flatcar-linux.org/releases/#stable-release
[rhel_7_7]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.7_release_notes/index
[rhel_7_8]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.8_release_notes/index
[rhel_7_9]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.9_release_notes/index
[rhel_8_2]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/8.2_release_notes/index
[rhel_8_4]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/8.4_release_notes/index
[RHCK]: https://docs.oracle.com/en/operating-systems/oracle-linux/7/relnotes7.9/
[ubuntu_18]: https://wiki.ubuntu.com/BionicBeaver/ReleaseNotes
[ubuntu_20]: https://wiki.ubuntu.com/FocalFossa/ReleaseNotes
[sles_15]: https://documentation.suse.com/en-us/sles/15-SP1/
