---
title: "Ping Sweep"
description: "Fast subnet ping sweep with logging. Outputs live and dead hosts to a CSV. Built for quick network discovery across MSP client sites."
icon: "///"
language: "Poweshell, Batch Script, or Bash Script"
github: "https://github.com/windlej/ping-sweep"
tags: ["python", "networking", "discovery"]
date: 2026-02-01
---

# Ping Sweep

## Description

Ping Sweep is a fast subnet ping sweep tool that logs live and dead hosts to a CSV file. It's built for quick network discovery across MSP client sites. Pass it a CIDR range, get back a list of live hosts.

## Features

-   Fast  and efficient ping sweeps.
-   Logging of live and dead hosts.
-   Outputs results to a CSV file.
-   Supports multiple operating systems: PowerShell, Command Prompt (Windows), and Bash (Linux/Mac).

## Installation

No installation is required. Simply download the appropriate script for your operating system from the  [GitHub repository](https://github.com/windlej/ping-sweep).

## Usage

### PowerShell (Windows)

1.  Save  `ping-sweep.ps1`  to a directory of your choice.
2.  Open PowerShell and navigate to the directory where you saved  `ping-sweep.ps1`.
3.  Run the script with the CIDR range as an argument:

```
.\ping-sweep.ps1 10.0.10.0/24

```

### Command Prompt (Windows)

1.  Save  `ping-sweep.bat`  to a directory of your choice.
2.  Open Command Prompt and navigate to the directory where you saved  `ping-sweep.bat`.
3.  Run the script with the CIDR range as an argument:

```
ping-sweep.bat 10.0.10.0/24

```

### Bash (Linux/Mac)

1.  Make sure  `nmap`  is installed on your system.
2.  Save  `ping-sweep.sh`  to a directory of your choice.
3.  Make the script executable:

```
chmod +x ping-sweep.sh

```

4.  Run the script with the CIDR range as an argument:

```
./ping-sweep.sh 10.0.10.0/24

```

### Output

The script outputs results to a CSV file named  `ping_sweep_results.csv`  in the same directory where the script is executed.

----------

## Dependencies

-   PowerShell:  None.
-   Command Prompt (Windows):  Built-in utilities.
-   Bash (Linux/Mac):  Requires  `nmap`.
