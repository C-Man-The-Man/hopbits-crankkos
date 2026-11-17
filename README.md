# Hopbits agents on CrankkOS

A community solution for running Hopbits agents (nodes) on CrankkOS gateways using Docker.

This project adapts the [official Hopbits documentation](https://hopbits.io/docs) to the CrankkOS environment, keeping persistent data under `/data` and supporting both Docker Run and Docker Compose.

**Unofficial community project. Not affiliated with or endorsed by Hopbits or Crankk.**

---

## Create a Hopbits account

Using my referral link if you find this useful:

### https://hopbits.io/register?ref=ST6XM6YL

---

## Quick setup — Docker Run

Run this single-line command on your CrankkOS gateway:

```bash
mkdir -p /data/hopbits/data && curl -fsSL https://hopbits.io/releases/Dockerfile -o /data/hopbits/Dockerfile && chown -R 65532:65532 /data/hopbits/data && chmod 700 /data/hopbits/data && docker build -t hopbits/agent:local /data/hopbits && docker run -d --name hopbits-agent --restart=always --cap-drop ALL --security-opt no-new-privileges:true --network host -e HOPBITS_NETWORK_MODE=host -v /data/hopbits/data:/var/lib/hopbits hopbits/agent:local && docker logs -f hopbits-agent
```

On your Hopbit Dashboard, pair the Hopbits agent with your account using the provided code from the logs.

Press `Ctrl+C` to exit the log viewer; the container will continue running.

---

## Docker Compose (recommended)

1. Create the necessary directories with the necessary permissions and navigate to the working one:

```bash
mkdir -p /data/hopbits/data && cd /data/hopbits
```

2. Download the official `Dockerfile`:

```bash
curl -fsSL https://hopbits.io/releases/Dockerfile -o /data/hopbits/Dockerfile
```

3. Download this repository's specific CrankkOS `docker-compose.yml`:

```bash
curl -fsSL https://raw.githubusercontent.com/C-Man-The-Man/hopbits-crankkos/main/docker-compose.yml -o /data/hopbits/docker-compose.yml
```

4. The agent runs as `UID/GID 65532:65532`, so give it ownership of the data directory:

```bash
chown -R 65532:65532 /data/hopbits/data && chmod 700 /data/hopbits/data
```

5. Build the Hopbits Docker image:

```bash
docker-compose build
```

6. Run the Hopbits container

```bash
docker-compose up -d
```

7. Check the logs and pair the agent with your account using the provided code:

```bash
docker-compose logs -f
```

Press `Ctrl+C` to exit the log viewer without stopping the container.


### Uninstall

Run each command individually in the working directory `/data/hopbits`:

```bash
docker-compose down -v
```

```bash
cd
```

```bash
rm -rf /data/hopbits
```

---

## Notes

- The official Hopbits Dockerfile is downloaded directly from [hopbits.io](https://hopbits.io/releases/Dockerfile) during setup.
- Persistent data is stored in `/data/hopbits/data`.
- The agent uses host networking, as specified in the official Docker instructions.
- This repository provides deployment instructions and configuration only; it does not contain the Hopbits agent.

---

## Donations

**Bitcoin wallet address**
```text
bc1qpcfex53u7mqx4dc25gw7j7446amw9vn6743cn5
```

**EVM / Metamask  (ETH, ETC, OCTA, POL, PEAQ, MONAD, BASE etc.)**
```text
0xbE4879888d95B02B2FCaed2FcAeBbcf36829BDC9
```

**Solana wallet address**
```text
7EHWvShXfjLJ2HhzTf4CsHgjKckivfMQMjnEoUAEqau
```

**Sui wallet address**
```text
0x421a5a462f99c2d675d035d0c741ba5765a47c1e28f95d33ad770cd34a36a6ea
```

**Thank you for your support!**
