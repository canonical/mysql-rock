# MySQL rock
[![Release to GHCR][release-badge]][release-link]

This repository contains the packaging metadata for creating a rock of MySQL built from
the official ubuntu MySQL package from the Ubuntu repository and further installs mysql-shell.
For more information on rocks, visit the [rockcraft repository][repo-rockcraft].

## Building the rock
The steps outlined below are based on the assumption that you are building the rock with the latest LTS of Ubuntu.
If you are using another version of Ubuntu or another operating system, the process may be different.

### Clone Repository
```bash
git clone https://github.com/canonical/mysql-rock.git
cd mysql-rock
```

### Installing Prerequisites
```bash
sudo snap install rockcraft --classic --edge
sudo snap install docker
sudo snap install lxd
```

### Configuring Prerequisites
```bash
sudo usermod -aG docker $USER 
sudo lxd init --auto
```

### Packing and Running the rock
```bash
rockcraft pack
rockcraft.skopeo --insecure-policy copy oci-archive:mysql*.rock docker-daemon:<username>/mysql:<tag>
docker run --rm -it <username>/mysql:<tag>
```

## License
The MySQL rock is free software, distributed under the Apache Software License, version 2.0.
See [LICENSE][repo-license].

[release-badge]: https://github.com/canonical/mysql-rock/actions/workflows/release.yaml/badge.svg
[release-link]: https://github.com/canonical/mysql-rock/actions/workflows/release.yaml
[repo-license]: https://github.com/canonical/mysql-rock/blob/8.0-24.04/LICENSE
[repo-rockcraft]: https://github.com/canonical/rockcraft
