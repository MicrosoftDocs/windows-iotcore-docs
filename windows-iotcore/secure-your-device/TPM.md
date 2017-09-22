---
title: Trusted Platform Module (TPM)
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn how to use a Trusted Platform Module to enable cryptographic capabilities to better secure devices.
keywords: windows iot, security, Trusted Platform Module, TPM, cryptography, keys
---

# Trusted Platform Module (TPM) on Windows 10 IoT Core

## What is TPM?
A Trusted Platform Module (TPM), is a cryptographic coprocessor including capabilities for random number generation, secure generation of cryptographic keys and limitation of their use. It also includes capabilities such as remote attestation and sealed storage.
TPM's technical specification is publicly available, driven by the Trusted Computing Group (TCG). The latest version TPM 2.0 (released October 2014), is a major redesign of the specification which adds new functionality and fixes weaknesses of the former TPM 1.2.

## Why TPM?  
Computers that incorporate a TPM can create cryptographic keys and encrypt them so that they can only be decrypted by the TPM. This process, often called **"wrapping"** or **"binding"** a key, can help protect the key from disclosure. Each TPM has a master "wrapping" key, called the storage root key, which is stored within the TPM itself. The private portion of a key created in a TPM is never exposed to any other component, software, process, or person.  

Computers that incorporate a TPM can also create a key that has not only been wrapped but is also tied to certain platform measurements. This type of key can only be unwrapped when those platform measurements have the same values that they had when the key was created. This process is called **"sealing"** the key to the TPM. Decrypting the key is called **"unsealing"**. The TPM can also seal and unseal data generated outside of the TPM. With this sealed key and software such as BitLocker Drive Encryption, you can lock data until specific hardware or software conditions are met.  

With a TPM, private portions of key pairs are kept separate from the memory controlled by the operating system. Keys can be sealed to the TPM, and certain assurances about the state of a system (assurances that define the "trustworthiness" of a system) can be made before the keys are unsealed and released for use. Because the TPM uses its own internal firmware and logic circuits for processing instructions, it does not rely on the operating system and is not exposed to vulnerabilities that might exist in the operating system or application software.

## TPM Architecture
_Difference between TPM 1.2 and TPM 2.0._  
The TPM specification has been developed twice. The first time, it developed from 1.1b to 1.2, incorporating  new capabilities requested/identified by the specification committee. This feature-creep form of evolution made the final TPM 1.2 specification very complicated. Eventually, cryptographic weaknesses of SHA-1 (which was the strongest commercial algorithm in TPM 1.2) were revealed which caused the need for a change. The TPM architecture was redesigned from scratch, resulting in the much more integrated and unified design of TPM 2.0.  

The changes and enhancements compared to the previous TPM 1.2 include:

* Support for additional cryptographic algorithms
* Enhancements to the availability of the TPM to applications
* Enhanced authorization mechanisms
* Simplified TPM management
* Additional capabilities to enhance the security of platform services

Note that Windows IoT Core supports only TPM 2.0 and does not support the outdated TPM 1.2.

## What is TBS? 
The TPM Base Services (TBS) feature is a system service that allows transparent sharing of the TPM resources. It shares the TPM resources among multiple applications on the same physical machine through remote procedure calls (RPC). It centralizes TPM access across applications using priorities specified by the calling applications.  

The TPM provides cryptographic functions designed to provide trust in the platform. Because the TPM is implemented in hardware, it has finite resources. The TCG defines a TPM Software Stack (TSS) that makes use of these resources to provide trusted operations for application software. However, no provision is made for running a TSS implementation side-by-side with operating system software that may also be using TPM resources. The TBS feature solves this problem by enabling each software stack that communicates with TBS to use TPM resources checking for any other software stacks that may be running on the machine.

## TPM solutions available on Windows IoT Core  
_A few words about Software TPM (sTPM), Firmware TPM (fTPM), Discrete TPM (dTPM)..._

### Firmware TPM (fTPM)  
Firmware TPM (fTPM) requires special Processor/SoC support that is not currently implemented on Raspberry Pi 2 or 3. MinnowBoard Max needs firmware version 0.80 or higher. DragonBoard410c provides fTPM capabilities out of the box enabled by default.  

### Discrete TPM (dTPM)  
Discrete TPM (dTPM) is considered the utmost trustworthy solution by all means.  
There are several manufacturers of dTPM chips and PCB modules that are supported on Windows IoT Core:

> [!div class="mx-tdBreakAll"]
> | TPM Manufacturer | Web Page|
> |-------------|----------|
> | Infineon | [Infineon Truted Computing](http://www.infineon.com/cms/en/product/security-ic/trusted-computing/channel.html?channel=db3a30433efacd9a013f10d2a7264daa)|
> | NationZ | [NationZ information](http://www.trustedcomputinggroup.org/nationz-technologies-inc)|
> | Nuvoton | [Nuvoton homepage](https://www.nuvoton.com/hq/products/cloud-computing/security/trusted-platform-module-tpm)|
> | STMicro | [STMicro TPM Secure MCUs](http://www.st.com/web/en/catalog/mmc/FM143/CL1814/SC1522)|

### Software TPM (sTPM)  
Software TPM (sTPM) is also referred to as TPM Simulator. It is platform-independent, supported on Windows IoT Core.  

> [!NOTE]
> sTPM is intended for development purposes only and does not provide any real security benefits.  


## Samples  
* [TBSSample project C++](https://developer.microsoft.com/en-us/windows/iot/samples/tbssample)
  This tutorial demonstrates how to create a basic C++ application that uses TBS to poll the TPM.  
* [Urchin Library Sample](https://developer.microsoft.com/en-us/windows/iot/samples/urchinlibrary) This tutorial demonstrates how to create a sample C++ application that exercises the TPM functionality using the [Urchin library](https://github.com/ms-iot/securit). Urchin is a spec-compliant library derived from the TPM 2.0 reference implementation. It provides to the client the functionality to marshal/unmarshal all data structures, properly calculate authorizations, perform parameter encryption and do auditing.

## Additional Resources  
* [Trusted Platform Module (TPM) Specifications](http://www.trustedcomputinggroup.org/developers/trusted_platform_module) 
* [TCG TPM 2.0 Library Specification](http://www.trustedcomputinggroup.org/resources/tpm_library_specification)
* [TPM Base Services](https://msdn.microsoft.com/en-us/library/windows/desktop/aa446796(v=vs.85).aspx) 
* [Enabling Secure Boot and BitLocker](SecureBootAndBitLocker.md)

