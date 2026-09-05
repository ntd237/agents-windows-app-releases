# Agents Windows Releases

[![Latest Release](https://img.shields.io/github/v/release/ntd237/agents-windows-app-releases?style=flat-square)](https://github.com/ntd237/agents-windows-app-releases/releases/latest)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![Last Updated](https://img.shields.io/github/last-commit/ntd237/agents-windows-app-releases?style=flat-square)](https://github.com/ntd237/agents-windows-app-releases/commits/main)

Public distribution channel for Agents Windows application: includes NSIS installers, security verification signatures, and automatic update manifests.

---

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Downloads](#downloads)
- [Installation](#installation)
- [Updates](#updates)
- [Repository Structure](#repository-structure)
- [Contact](#contact)

---

## Introduction

This repository serves as a public distribution channel for the **Agents Windows** application.

### Main Purpose

- **Secure Distribution**: Provide digitally signed and verified installers
- **Automatic Updates**: Support in-app update mechanism through `latest.json` manifest
- **Security**: Use minisign to sign installer files, ensuring integrity and authenticity

### Important Notes

- **Private Source Code**: The main application repository is kept private
- **Release Assets Only**: This repository stores only release files (installers, signatures, manifests)
- **Automated Releases**: Releases are generated automatically from the CI/CD pipeline

---

## Features

### Basic Features
- 64-bit Windows installer (`.exe`)
- Security verification signature (`.sig`)
- Automatic update manifest (`latest.json`)

### Security Features
- Signature verification using minisign
- Enhanced reliability during installation
- Detection of modified or counterfeit files

---

## Downloads

### How to Download the Latest Installer

Download the latest version from [Releases](https://github.com/ntd237/agents-windows-app-releases/releases/latest):

```
https://github.com/ntd237/agents-windows-app-releases/releases/latest
```

### Available Files

Each release includes:

| File | Description |
|------|-------------|
| `Agents.Windows_X.X.X_x64-setup.exe` | Windows installer (64-bit) |
| `Agents.Windows_X.X.X_x64-setup.exe.sig` | Security verification signature (minisign) |
| `latest.json` | Update manifest for the application |

---

## Installation

### System Requirements

- Windows 10 or later (64-bit)
- Administrator privileges for installation
- Internet connection (for downloading)

### Installation Guide

#### Step 1: Download the Installer

Download the `Agents.Windows_X.X.X_x64-setup.exe` file from [Releases](https://github.com/ntd237/agents-windows-app-releases/releases/latest).

#### Step 2: Verify Signature (Optional but Recommended)

To verify the integrity of the installer:

1. Install [minisign](https://jedisct1.github.io/minisign/)
2. Download the signature `Agents.Windows_X.X.X_x64-setup.exe.sig`
3. Run the verification command:

```bash
minisign -Vm Agents.Windows_X.X.X_x64-setup.exe -P <public-key>
```

*(The public key will be provided in the Security section)*

#### Step 3: Run the Installer

1. Double-click the `.exe` file to launch the installer
2. Follow the on-screen instructions
3. Select installation location or accept the default
4. Complete the installation

#### Step 4: Verify Installation

After installation is complete:

1. Find "Agents" in the Start menu
2. Launch the application
3. Check the version in Help → About

---

## Updates

### Automatic Updates

The **Agents Windows** application supports automatic updates:

1. The application checks the `latest.json` file from this repository
2. If a new version is available, users will be notified
3. Click the "Update" button to download and install the new version

### Manual Updates

If automatic updates don't work:

1. Download the latest installer from [Releases](https://github.com/ntd237/agents-windows-app-releases/releases/latest)
2. Run the installer (it will overwrite the old version)
3. Restart the application if needed

---

## Repository Structure

```
agents-windows-app-releases/
├── README.md                          # Documentation (Vietnamese)
├── README_EN.md                       # Documentation (English)
└── releases/                          # Release files (automatically managed)
    ├── v0.1.2/
    │   ├── Agents.Windows_0.1.2_x64-setup.exe
    │   ├── Agents.Windows_0.1.2_x64-setup.exe.sig
    │   └── latest.json
    └── ...
```

### Main Files

| File | Purpose |
|------|---------|
| `README.md` | Documentation and guide (Vietnamese) |
| `README_EN.md` | Documentation and guide (English) |
| `.exe` | Windows installer |
| `.sig` | Verification signature (minisign) |
| `latest.json` | Latest version manifest |

---

## Contact

**Author**: ntd237

- **Email**: ntd237.work@gmail.com
- **GitHub**: [@ntd237](https://github.com/ntd237)

If you have any questions or discover issues related to the releases, please open an [Issue](https://github.com/ntd237/agents-windows-app-releases/issues).
