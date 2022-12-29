<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="#">
    <img src="https://www.divalabs.org/logoFull.svg" alt="Logo" width="200" height="80">
  </a>
  <p align="center">
    Liquid Staking protocol powered by Distributed Validators
    <br />
  </p>
</div>

<!-- ABOUT THE PROJECT -->
## About Diva Private Testnet
You are lucky enough to access to our very first version of the private testnet which surely has a lot of bugs, typos, and room for improvement. So please, let us know anything you believe it could make diva better. 
For your convenience, we are packing everything for the testnet in a docker including the execution and consensus clients along with diva's. The tesnet includes:

- [x] P2P
- [x] Validation in Goerli
- [x] Own Ethereum clients for Goerli
- [x] UI
    - [x] Stakers UI
    - [x] Operators UI
- [x] LSD
    - [ ] Rebasing
- [ ] DKG (coming soon)
- [ ] Oracle (coming soon)


## Instructions
### Prerequisites
To be able to follow these instructions and sucessfully run a node, you will need the following:

- Hardware with enough resources for running an Ethereum Validator: XXX Gb, ...??
- Supported platforms are Ubuntu, ....???
- Manual Credentials provided by Diva (these are needing during the testnet-zero phase):
  - One custom ``NODEID``
  - One or more custom ``KEYSHARE``
  - If you don't have these, please ask for them – you'll need them


### Installation

  1. Docker needs to be installed along with the compose plugin.
   
  [Click here for the installation instructions for Ubuntu](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
  
  2. Give permissions to your user to run docker:
```
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

3. Then clone this github repository to download the Docker image:
  ```
  git clone https://github.com/vadie22/zero.git && cd zero
  ```

4. Now load the Diva Docker image

```
docker load -i diva.tar 
```
You will see a message confirming that the image has been loaded.

5. Run the compose:
```
docker compose up -d
```

Your clients will start syncing. Meanwhile, you can emulate the registration that very soon will be done automatically by diva.

### Manual Registration (testnet-zero only)


6. Delete the node identity:
```
curl --location --request DELETE 'http://localhost:80/api/v1/keymanager/node-key'
```
7. Install as many Key-Shares as you have, relace the values for KEYSHARE:
```
curl --location --request PUT 'http://localhost:80/api/v1/keymanager/signing-key' \
--header 'Authorization: Bearer SECRET_AUTHq_TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "secret_key": "KEYSHARE"
}'
```
8. Register the node, replace the values for NODEID:

```
curl --location --request POST 'http://localhost:80/api/v1/keymanager/node-key' \
--header 'Content-Type: application/json' \
--data-raw '{
    "secret_key": "NODEID"
}'
```

### USAGE

Access to your dashboard from a browser: ``http://YOUR_PUBLIC_IP/#/dashboard``

You can also:

- ``docker logs zero-geth-1`` to view the Geth Ethereum Execution Client logs (add ``-f`` for streaming logs)
- ``docker logs zero-teku-1`` to view the Teku Ethereum Consensus Client logs (add ``-f`` for streaming logs)
