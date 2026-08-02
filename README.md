# RetPlan releases

Signed Windows installers for **RetPlan**, a retirement planner for Windows.

This repository contains **no source code**. It exists so that Windows App Installer, which
fetches anonymously, can reach the installer and update manifest over a permanent public URL.

- Product and documentation: <https://retplan.azurewebsites.net>
- Free web app (no install): <https://retplan.azurewebsites.net/app/>

## Install

Download and open the `.appinstaller` for your architecture. Windows registers the app for
automatic updates and checks for a new version every 12 hours.

| Architecture | Installer |
|---|---|
| x64 | [RetPlan.appinstaller](https://github.com/francisab/retplan-releases/releases/latest/download/RetPlan.appinstaller) |
| Arm64 | [RetPlan-arm64.appinstaller](https://github.com/francisab/retplan-releases/releases/latest/download/RetPlan-arm64.appinstaller) |

Not sure which you need: **Settings → System → About → System type**.

The packages are signed by Azure Trusted Signing and chain to a certificate authority Windows
already trusts, so **no certificate import is required**. SmartScreen may still warn until the
signing identity accumulates reputation.

Each release also publishes `version.json` with the version, per-architecture size and SHA-256,
so you can verify a download:

```powershell
Get-FileHash .\RetPlan.msix -Algorithm SHA256
```

## Access is currently limited

RetPlan is in a **private preview**. Anyone can install the app, but signing in requires an
account that has been provisioned in advance, and the app cannot be used without signing in.
Installing without a provisioned account will leave you at the sign-in screen.

## Upgrading from a build installed before 1 August 2026

Earlier packages were published under a different signing identity. Windows treats a publisher
change as a different application and will refuse to upgrade in place, so remove the old
install first:

```powershell
Get-AppxPackage *RetPlan* | Remove-AppxPackage
```

Plans are stored in your own `.rpd` file and are not affected by uninstalling.

## Issues

Please report problems through the product site. This repository does not track issues for the
application itself.
