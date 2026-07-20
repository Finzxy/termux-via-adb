# Accessing the Termux Environment via ADB (No Root Required)

This guide explains how to access the Termux user environment from an active Android Debug Bridge (ADB) shell session **without requiring root access**. By leveraging Android's `run-as` command, you can execute commands within the Termux application sandbox while preserving the application's user environment.

> **Note**
>
> This method works only if the installed version of Termux supports the `run-as` command. No root privileges or modifications to the Android system are required.

## Prerequisites

Before proceeding, ensure that the following requirements are met:

* Termux is installed on the target Android device.
* USB Debugging or Wireless Debugging is enabled.
* An active ADB connection has been established.
* An interactive shell has been opened using `adb shell`.

## Launch the Termux Shell

Execute the following command to start the Termux Bash shell within the application's sandbox:

```bash
run-as com.termux /data/data/com.termux/files/usr/bin/bash
```

## Configure the Environment

Since the default ADB shell does not inherit the Termux environment, add the Termux binary directory to the `PATH` variable:

```bash
export PATH=/data/data/com.termux/files/usr/bin:$PATH
```

This makes all Termux-installed executables (such as `pkg`, `git`, `python`, and others) available in the current session.

## Change to the Home Directory

Navigate to the default Termux home directory:

```bash
cd /data/data/com.termux/files/home
```

The shell is now configured to behave similarly to a standard Termux session.

## Verification

Verify that the environment has been initialized correctly:

```bash
pwd
```

Expected output:

```text
/data/data/com.termux/files/home
```

To verify that the Termux binaries are being used:

```bash
which bash
which pkg
```

Expected output:

```text
/data/data/com.termux/files/usr/bin/bash
/data/data/com.termux/files/usr/bin/pkg
```

## Quick Start

```bash
run-as com.termux /data/data/com.termux/files/usr/bin/bash
export PATH=/data/data/com.termux/files/usr/bin:$PATH
cd /data/data/com.termux/files/home
```
