# letsencrypt-win
An [ACME](https://github.com/letsencrypt/acme-spec) client library and PowerShell module interoperable with the [Let's Encrypt](https://letsencrypt.org/) reference implemention [ACME Server](https://github.com/letsencrypt/boulder) and comparable to the feature set of the corresponding [client](https://github.com/letsencrypt/letsencrypt). 

The PowerShell modules include installers for configuring:
* IIS 7.0+ either locally or remotely (over PSSession)
* AWS Server Certificates and ELB Listeners

--

[![Build status](https://ci.appveyor.com/api/projects/status/0knwrhni528xi2rs?svg=true)](https://ci.appveyor.com/project/ebekker/letsencrypt-win)


---

## Overview

This ACME client implementation is broken up into layers that build upon each other:
* Basic tools and service required for implementing ACME protocol (JSON Web Signature (JWS), persistence, PKI operations via OpenSSL) (.NET assembly)
* A low-level ACME protocol client that can interoperate with a proper ACME server (.NET assembly)
* A PowerShell Module that implements a "local vault" for managing ACME Registrations, Identifiers and Certificates (PS Binary Module)
* A set of PowerShell Modules that implement installers for various servers/services (PS Script Modules)
  * IIS Installer
  * AWS Installer
  * Futuer Installers...

This ACME client is being developed against the [Boulder CA](https://github.com/letsencrypt/boulder) ACME server reference implementation.  See how to [quickly spin up your own instance](https://github.com/ebekker/letsencrypt-win/wiki/Setup-Boulder-CA-on-Amazon-Linux) in AWS on an **Amazon Linux AMI**.

---

## Current State

This client is now operable and can successfully interact with the Let's Encrypt  [staging CA](https://acme-staging.api.letsencrypt.org/) to initialize new Registrations, authorize DNS Identifiers and issue Certificates.  Further, it can succussfully install and configure the certificate and related SSL settings for a local or remote IIS 7.0+ server or an AWS environment.

## Example Operations

Here is a typical usage scenario based on the _current_ state of the project.

```
## In PowerShell console
mkdir c:\Vault
cd c:\Vault
Import-Module ACMEPowerShell
Initialize-ACMEVault
```

