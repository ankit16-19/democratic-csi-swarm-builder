![Cloud Skeleton](./assets/logo.jpg)

[![GPLv3 License](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE) [![OS: Ubuntu_≥24.04](https://img.shields.io/badge/OS-Ubuntu_≥24.04-orange.svg)]() [![Tool: GitHub Actions](https://img.shields.io/badge/Tool-GitHub_Actions-blue.svg)]()

# **[Cloud Skeleton][cloud-skeleton]** ► **[Democratic CSI Swarm Builder][democratic-csi-swarm-builder]**

## Overview

The **[Democratic CSI Swarm Builder][democratic-csi-swarm-builder]** repository provides a **[GitHub Actions][github-actions]** workflow that automatically:

1. **Detects** the latest `democraticcsi/democratic-csi` image on **[Docker Hub][docker-hub]**  
2. **Extracts** its filesystem into a **[Docker Swarm-compatible][docker-swarm]** plugin bundle  
3. **Packages** it (with `config.json` CSI manifest) as a **[Docker Plugin][docker-plugin]**  
4. **Publishes** versioned and `latest` tags to **GitHub Container Registry (GHCR)**  

This makes the **[Democratic CSI][democratic-csi]** driver installable in **[Docker Swarm][docker-swarm]** with a simple:

```bash
docker plugin install --grant-all-permissions \
  ghcr.io/cloud-skeleton/democratic-csi-swarm:latest
```

> **Tip:**  
> Before installing plugin create configuration for **[Democratic CSI][democratic-csi]** on host system path `/etc/democratic-csi.yml`.
>
> Example for Synology devices behind reverse proxy:
>
> ```yaml
> driver: synology-iscsi
>
> httpConnection:
>   host: <HOSTNAME>
>   password: <PASSWORD>
>   port: 443
>   protocol: https
>   serialize: true
>   session: democratic-csi
>   username: <USERNAME>
>
> iscsi:
>   baseiqn: iqn.2025-07.<REVERSE DOMAIN>:democratic-csi.
>   lunSnapshotTemplate:
>     is_app_consistent: true
>     is_locked: true
>   lunTemplate:
>     type: BLUN
>   targetPortal: <HOSTNAME>
>   targetTemplate:
>     auth_type: 0
>     max_sessions: 0
>
> # Until merged https://github.com/democratic-csi/democratic-csi/pull/501
> node:
>   format:
>     ext4:
>       customOptions:
>         - -E
>         - nodiscard
> ```
>

---

## Contributing

Contributions and improvements to this installation script are welcome!  
- Fork the repository.  
- Create a new branch (e.g., **`feature/my-improvement`**).  
- Submit a pull request with your changes.

## License

This project is licensed under the [GNU General Public License v3.0](LICENSE).

---

*This repository is maintained exclusively by the **[Cloud Skeleton][cloud-skeleton]** project, and it was developed by EU citizens who are strong proponents of the European Federation. 🇪🇺*

<!-- References -->
[cloud-skeleton]: https://github.com/cloud-skeleton/  
[democratic-csi]: https://github.com/democratic-csi/democratic-csi/tree/master/examples
[democratic-csi-swarm-builder]: https://github.com/cloud-skeleton/democratic-csi-swarm-builder/  
[docker-hub]: https://docs.docker.com/docker-hub/quickstart/  
[docker-plugin]: https://docs.docker.com/engine/extend/#developing-a-plugin  
[docker-swarm]: https://docs.docker.com/engine/swarm/  
[github-actions]: https://docs.github.com/en/actions/get-started/quickstart
