# Scylla DB Setup guide
[^references]: [Scylla Installation guide](https://docs.scylladb.com/operating-scylla/manager/2.0/install/#system-requirements)
Changed in version 2.0: Scylla Manager

## System requirements
Scylla Manager Server has modest systems requirements. While a minimal server can run on a system with 2 cores and 1GB RAM, the following configuration is recommended:
* **CPU** - 2vCPUs
* **Memory** - 8GB+ DRAM

## Installation workflow
1.   Install Scylla Manager
2.   Run the scyllamgr_setup script
3.   Enable Bash Script Completion
4.   Start Scylla Manager Service and verify Scylla Manager is Running and that sctool is running


## Install Scylla Manager
Choose one of the following installation methods:

### Scylla Manager for Scylla Enterprise

1.  Download and install Scylla Manager from the Enterprise Download page.
2.  Follow the entire installation procedure.
3.  Continue with Run the scyllamgr_setup script.

### Scylla Manager for Scylla Open Source

1.    On the same node as you are installing Scylla Manager, download and install Scylla as a local database from the Scylla Open Source Download page. There is no need to run the Scylla setup as it is taken care of by the scyllamgr_setup script.
2.   Download and Install Scylla Manager from the Scylla Manager Open Source Download page.
3.    Follow the entire installation procedure.
4.    Continue with Run the scyllamgr_setup script.


### Run the scyllamgr_setup script

The Scylla Manager setup script automates the configuration of Scylla Manager by asking you some simple questions. It can be run in non-interactive mode if you’d like to script it.

There are three decisions you need to make:

*   Do you want to enable the service to start automatically? If not, you will have to start the service manually each time you want to use it.
*   Do you want to set up and enable a local Scylla backend? If not, you will need to set up a remote DB
*   Do you want Scylla Manager to check periodically if updates are available? If not, you will need to check yourself.


```java
 scyllamgr_setup -h
Usage: scyllamgr_setup [-y][--no-scylla-setup][--no-enable-service][--no-check-for-updates]

Options:
  -y, --assume-yes          assume that the answer to any question which would be asked is yes
  --no-scylla-setup         skip setting up and enabling local Scylla instance as a storage backend for Scylla Manager
  --no-enable-service       skip enabling service
  --no-check-for-updates    skip enabling periodic check for updates
  -h, --help                print this help

Interactive mode is enabled when no flags are provided.
```


### Procedure

1.  Run the scyllamgr_setup script to configure the service. You can run the script in interactive mode (no flags) or automate your decision making by using flags.

### Enable bash script completion

Enable bash completion for sctool: the Scylla Manager CLI. Alternatively, you can just open a new terminal.
 
```java
source /etc/bash_completion.d/sctool.bash
```

## Start Scylla Manager service
Scylla Manager integrates with systemd and can be started and stopped using ```java systemctl``` command.

### Procedure

1. Start the Scylla Manager server service.

```java
sudo systemctl start scylla-manager.service
```

2. Verify the Scylla Manager server service is running.

```java
sudo systemctl status scylla-manager.service
● scylla-manager.service - Scylla Manager Server
   Loaded: loaded (/usr/lib/systemd/system/scylla-manager.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2019-10-30 11:00:01 UTC; 20s ago
 Main PID: 5805 (scylla-manager)
   CGroup: /system.slice/scylla-manager.service
           └─5805 /usr/bin/scylla-manager

...

Hint: Some lines were ellipsized, use -l to show in full.
```
3. Confirm sctool is running by displaying the sctool version.

```java
sctool version
Client version: 2.0-0.20191030.9442dd9b
Server version: 2.0-0.20191030.9442dd9b
```



