---
title: bitsadmin setreplyfilename
description: "Windows Commands topic for **bitsadmin setreplyfilename** - Specify the path of the file that contains the server reply."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bitsadmin setreplyfilename

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Specify the path of the file that contains the server reply.
## Syntax
```
bitsadmin /SetReplyFileName <Job> <path>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
|path|Location to place the server reply|
## remarks
Valid only for upload-reply jobs.
## <a name="BKMK_examples"></a>Examples
The following example sets the reply filename pathfor the job named *myDownloadJob*.
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)