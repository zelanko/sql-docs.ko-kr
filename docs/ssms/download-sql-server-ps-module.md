---
title: "SQL Server PowerShell 모듈 다운로드 | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords: "sql server powershell 설치, sql server powershell 다운로드"
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 208bf291819a3e847e784e76611acdec0bf2f2d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="download-sql-server-powershell-module"></a>SQL Server PowerShell 모듈 다운로드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] SQL Server Management Studio의 17.0 릴리스의 일환으로 SQL Server PowerShell 모듈이 이제 PowerShell 갤러리를 통해 제공됩니다.  이 모듈은 더 이상 SSMS 설치 패키지에 포함되지 않습니다. SSMS 17.0 버전 이상에서 PowerShell을 사용하려면 추가 단계로 SQL Server 모듈을 컴퓨터에 설치해야 합니다.

Windows Management Framework의 최신 버전 설치에 대한 전체 설명서와 PowerShell 모듈 설치 방법에 대한 일반적인 내용은 [PowerShell 갤러리](https://www.powershellgallery.com/) 사이트를 참조하세요.

SQL Server 모듈을 설치하는 PowerShell 명령은 다음과 같습니다.

> Install-Module -Name SqlServer

이 명령은 컴퓨터의 모든 사용자에 대한 모듈을 설치합니다. 관리자 권한으로 PowerShell 프로세스를 실행해야 합니다.

> Install-Module -Name SqlServer -Scope CurrentUser

이 명령은 현재 PowerShell 프로세스를 실행 중인 사용자를 위한 모듈을 설치합니다. 관리자 권한으로 PowerShell 프로세스를 실행할 필요가 없습니다.

컴퓨터에 SQL Server PowerShell 모듈의 이전 버전이 있는 경우 “-AllowClobber” 매개 변수를 제공해야 할 수 있습니다.  

관리자 권한으로 실행 중이고 컴퓨터의 모든 사용자를 위해 모듈을 설치하는 경우

> Install-Module -Name SqlServer -AllowClobber

관리자 권한으로 실행할 수 없거나 현재 사용자를 위해서만 설치하는 경우

> Install-Module -Name SqlServer -Scope CurrentUser -AllowClobber

업데이트된 버전의 SqlServer 모듈을 사용할 수 있는 경우 Update-Module 명령을 사용하여 버전을 업데이트할 수 있게 됩니다.

> Update-Module -Name SqlServer

컴퓨터에 설치된 모듈의 버전을 보려면 다음을 사용할 수 있습니다.

> Get-Module SqlServer -ListAvailable

스크립트에서 모듈의 특정 버전을 사용하려면 다음과 같이 가져올 수 있습니다.

> Import-Module SqlServer -Version 21.0.17178

PowerShell 갤러리에 제공되는 SQL Server PowerShell 모듈 버전은 버전 관리를 지원하며 PowerShell 버전 5.0 이상이 필요합니다. [PowerShell 갤러리](https://www.powershellgallery.com/packages/Sqlserver/)에서 SqlServer 모듈을 찾을 수 있습니다. 
