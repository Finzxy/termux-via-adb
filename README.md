# Accessing the Termux Environment via ADB (No Root Required)

This guide shows how to access the Termux environment from an ADB shell without requiring root privileges.

> [!NOTE]
> This method uses Android's `run-as` command and only works with Termux versions that support it.

<p align="center">
  <img src="Screenshot from 2026-07-20 09-35-03.png" alt="Termux running inside ADB shell" width="800">
</p>

## Requirements

Before you begin, make sure you have:

* Termux installed on your Android device.
* USB Debugging or Wireless Debugging enabled.
* An active ADB connection.
* An interactive `adb shell` session.

## 1. Launch the Termux Shell

Run the following command inside the ADB shell:

```bash
run-as com.termux /data/data/com.termux/files/usr/bin/bash
```

## 2. Configure the Environment

Add the Termux binary directory to your `PATH`:

```bash
export PATH=/data/data/com.termux/files/usr/bin:$PATH
```

This allows you to use all Termux commands, including `pkg`, `git`, `python`, and other installed packages.

## 3. Change to the Home Directory

Switch to the default Termux home directory:

```bash
cd /data/data/com.termux/files/home
```

You are now working inside the Termux environment.

## Verify the Environment

Check your current working directory:

```bash
pwd
```

Expected output:

```text
/data/data/com.termux/files/home
```

Verify that the Termux binaries are being used:

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
