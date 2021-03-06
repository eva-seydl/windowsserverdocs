---
title: Add host information for TPM-trusted attestation
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 03/02/2017
---

>Applies To: Windows Server 2016

### Add host information for TPM-trusted attestation

For TPM mode, the fabric administrator captures three kinds of host information, each of which needs to be added to the HGS configuration:

- A TPM identifier (EKpub) for each Hyper-V host
- Code Integrity policies, a white list of allowed binaries for the Hyper-V hosts
- A TPM baseline (boot measurements) that represents a set of Hyper-V hosts that run on the same class of hardware

The process that the fabric administrator uses is described in [TPM-trusted attestation for a guarded fabric - capturing information required by HGS](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#capture-hardware-and-software-information). 

After the fabric administrator captures the information, add it to the HGS configuration as described in the following procedure.

1.  Obtain the XML files that contain the EKpub information and copy them to an HGS server. There will be one XML file per host. Then, in an elevated Windows PowerShell console on an HGS server, run the command below. Repeat the command for each of the XML files.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName> -Force
    ```
    
    >**Note**&nbsp;&nbsp;The **-Force** flag is used here to bypass a validation of the EKcert of the host's TPM. Hosts using TPMs without an EKcert or with an EKcert issued by an authority your HGS server does not trust will throw an error without the use of -Force. For the highest level of security, do not use the -Force flag, so that you will be alerted to potentially untrustworthy TPMs.

2. Obtain the code integrity policy that the fabric administrator created for the hosts, in binary format (*.p7b). Copy it to an HGS server. Then run the following command.

    For `<PolicyName>`, specify a name for the CI policy that describes the type of host it applies to. A best practice is to name it after the make/model of your machine and any special software configuration running on it.<br>For `<Path>`, specify the path and filename of the code integrity policy.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

3. Obtain the TCGlog file that the fabric administrator captured from a reference host. Copy the file to an HGS server. Then run the following command. Typically, you will name the policy after the class of hardware it represents (for example, "Manufacturer Model Revision").

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

This completes the process of configuring an HGS cluster for TPM mode. The fabric administrator might need you to provide two URLs from HGS before the configuration can be completed for the hosts. To obtain these URLs, on an HGS server, run [Get-HgsServer](https://technet.microsoft.com/library/mt652162.aspx).

