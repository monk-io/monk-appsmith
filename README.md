# AppSmith meets Monk

This repository contains Monk.io template to deploy AppSmith system either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

- [AppSmith meets Monk](#appsmith-meets-monk)
  - [Prerequisites](#prerequisites)
    - [Make sure monkd is running](#make-sure-monkd-is-running)
    - [Clone Repository](#clone-repository)
    - [Update configuration](#update-configuration)
    - [Load Template](#load-template)
    - [Verify if it's loaded correctly](#verify-if-its-loaded-correctly)
  - [Deploy appsmith](#deploy-appsmith)
  - [Stop, remove and clean up workloads and templates](#stop-remove-and-clean-up-workloads-and-templates)

## Prerequisites

- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

### Make sure monkd is running

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

### Clone Repository

```bash
git clone git@github.com:monk-io/monk-appsmith.git
```

### Update configuration

This template has very basic AppSmith configuration and will start a running copy of AppSmith, however it is most desired that you would update it with the configuration you would need.
To do so edit the `manifest.yaml` and in the `files` section replace the config provided with yours.
You could also use a `contents: <<< AppSmith.conf` notation to read the contents of the file instead of providing it in-line.

### Load Template

```bash
cd monk-appsmith
monk load manifest.yaml
```

### Verify if it's loaded correctly

```bash
$ monk list -l appsmith
✔ Got the list
Type      Template     Repository  Version  Tags
runnable  appsmith/server  local       -        -
```

## Deploy appsmith

```bash
$ monk run appsmith/server
✔ Starting the job: local/appsmith/server... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% ghcr.io/akafeng/appsmith:2.0.9 local
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Started local/appsmith/server

🔩 templates/local/appsmith/server
 └─🧊 Peer local
    └─🔩 templates/local/appsmith/server
       └─📦 202f7b9e6ac73bb380e9de0464ca4593-local-appsmith-server-appsmith4
          ├─🧩 ghcr.io/akafeng/appsmith:2.0.9
          └─🔌 open tcp 1.1.1.1:179 -> 179

💡 You can inspect and manage your above stack with these commands:
        monk logs (-f) local/appsmith/server - Inspect logs
        monk shell     local/appsmith/server - Connect to the container's shell
        monk do        local/appsmith/server/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Stop, remove and clean up workloads and templates

```bash
monk purge    AppSmith/server
monk purge -x AppSmith/server
```
