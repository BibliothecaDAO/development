---
sidebar_position: 2
---

# Docker Setup

(This only works if you have Docker installed)

---

# Get account address & private key

Install the [Argent X wallet](https://www.argent.xyz/argent-x/) and create an account. Export your private key from Argent X. Take note of your private key and account address as these will be needed to replace the `PRIVATE_KEY` and `ACCOUNT_ADDRESS` placeholders below.

---

# Build Image

Save the following Dockerfile in a new local directory

```dockerfile
FROM ghcr.io/bibliothecaforadventurers/loot:latest

ARG STARKNET_PRIVATE_KEY
ENV STARKNET_PRIVATE_KEY=$STARKNET_PRIVATE_KEY
ARG STARKNET_ACCOUNT_ADDRESS
ENV STARKNET_ACCOUNT_ADDRESS=$STARKNET_ACCOUNT_ADDRESS
ARG STARKNET_NETWORK
ENV STARKNET_NETWORK=${STARKNET_NETWORK:-alpha-goerli}
ENV MAX_FEE=1000000000000000

WORKDIR /loot/realms-contracts/
RUN /bin/bash -c "source scripts/setup_cli_env.sh"

ENTRYPOINT ["nile"]
```

In the directory you saved the Dockerfile, run the following command to build your Docker image. Replace the placeholders with the values from the previous section.

⚠️ Never expose this image you've built to the public since your private keys can be seen in docker history!

```
docker build \
  --build-arg STARKNET_PRIVATE_KEY=<PRIVATE_KEY> \
  --build-arg STARKNET_ACCOUNT_ADDRESS=<ACCOUNT_ADDRESS> \
  . -t realms_cli
```
---

# Run Actions


```bash
# list available actions
docker run -t realms_cli

# run check_resources action
docker run -t realms_cli check_resources

# get shell access
docker run -it --entrypoint /bin/bash realms_cli

```
