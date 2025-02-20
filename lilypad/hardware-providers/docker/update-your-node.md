---
description: >-
  Instructions to update your Docker node for Resource Providers who already had
  Lilypad installed.
---

# Update Your Node

## Remove Previous Versions

If the Linux Install was your previous version, follow part A, and if you had previously installed a Docker version, follow part B if you have already installed the Docker version and are updating.\


### A) Ensure all processes from Linux install are stopped and removed

_This only applies if you had a Linux version installed_

1. Stop all systemd  processess

```bash
sudo systemctl stop bacalhau
```

```bash
sudo systemctl stop lilypad-resource-provider
```

2. Disable the systemd services:

```bash
sudo systemctl disable bacalhau
```

```bash
sudo systemctl disable lilypad-resource-provider
```

3. Delete the service files from the systemd directory.

_\*\*Note: Be extremely careful when using `sudo` to remove files._

```bash
sudo rm /etc/systemd/system/bacalhau.service
```

```bash
sudo rm /etc/systemd/system/lilypad-resource-provider.service
```

3. Reload the systemd daemon to apply the changes.

```bash
sudo systemctl daemon-reload
```

### B) Remove old Docker containers <a href="#update-lilypad-version-for-docker-rp" id="update-lilypad-version-for-docker-rp"></a>

1. If a Docker RP is running stop the system (if the node is not running, disregard this first step)

```bash
docker compose down
```

2. You can check the status of the containers with:

```
docker ps -a | grep -E "resource-provider|ipfs|watchtower"
```

If they are running, stop them with:

```
docker stop <container_name>
```

&#x20;Remove the containers:

```
docker rm <container_name>
```

2. View all Docker images

```bash
docker images
```

3. Take note of all the IMAGE ID for each lilypad image (resource-provider, bacalhau, and watchtower)&#x20;

Delete old Docker images that are duplicates for Lilypad (Bacalhau, Lilypad)

```bash
docker rmi <IMAGE ID>  
```

\*_Note - You can also use  `docker volume prune` to remove specific images that aren't being used_



## Install and Run a new Version of Lilypad

1. Create a new Resource Provider wallet (_We recommend you don't use the same one you were using before, and you cannot use the same wallet you use to run jobs_). See the Docs for [Setting up a Metamask Wallet](../../lilypad-testnet/quick-start/setting-up-metamask.md)
2. Export your new WEB3\_PRIVATE\_KEY as an environment variable

```bash
export WEB3_PRIVATE_KEY=<your-private-key>
```

3. Use `curl` to download the `docker-compose.yml` file from the Lilypad GitHub repository.

```
LATEST_VERSION=$(curl -s https://api.github.com/repos/Lilypad-Tech/lilypad/releases/latest | sed -n 's/.*"tag_name": "\(.*\)".*/\1/p')

curl -o docker-compose.yml "https://raw.githubusercontent.com/Lilypad-Tech/lilypad/$LATEST_VERSION/docker/docker-compose.yml"
```

4. Start your Lilypad Node

```bash
WEB3_PRIVATE_KEY=<your_private_key> docker compose up -d
```

OR start with your own RPC URL

```bash
WEB3_PRIVATE_KEY=<your_private_key> WEB3_RPC_URL=wss://arb-sepolia.g.alchemy.com/v2/your-alchemy-id docker compose up -d
```

### Monitor Your Node <a href="#id-5.-monitor-your-node" id="id-5.-monitor-your-node"></a>

Use the following command to check the status of the resource provider and bacalhau.

```
docker logs resource-provider
```

```
docker logs bacalhau
```

Use the following command to view the containers running after starting Docker Compose.

```
docker ps
```

A healthy, updated node should have all containers started, a preflight check, and be adding a resource offer.\


<figure><img src="../../.gitbook/assets/Screenshot from 2025-02-19 09-40-43.png" alt=""><figcaption><p>An updated Lilypad node output</p></figcaption></figure>
