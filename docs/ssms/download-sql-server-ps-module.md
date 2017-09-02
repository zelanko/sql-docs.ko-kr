---
title: "SQL Server PowerShell 모듈 다운로드 | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "sql server powershell 설치, sql server powershell 다운로드"
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="download-sql-server-powershell-module"></a>SQL Server PowerShell 모듈 다운로드
SQL Server Management Studio의 17.0 릴리스의 일환으로 SQL Server PowerShell 모듈이 이제 PowerShell 갤러리를 통해 제공됩니다.  이 모듈은 더 이상 SSMS 설치 패키지에 포함되지 않습니다. SSMS 17.0 버전 이상에서 PowerShell을 사용하려면 추가 단계로 SQL Server 모듈을 컴퓨터에 설치해야 합니다.

Windows Management Framework의 최신 버전 설치에 대한 전체 설명서와 PowerShell 모듈 설치 방법에 대한 일반적인 내용은 [PowerShell 갤러리](https://www.powershellgallery.com/) 사이트를 참조하세요.

SQL Server 모듈을 설치하는 PowerShell 명령은 다음과 같습니다.

> Install-module -Name SqlServer -Scope CurrentUser

컴퓨터에 SQL Server PowerShell 모듈의 이전 버전이 있는 경우 “-AllowClobber” 매개 변수를 제공해야 할 수 있습니다.  

PowerShell 갤러리에 제공되는 SQL Server PowerShell 모듈 버전은 버전 관리를 지원하며 PowerShell 버전 5.0 이상이 필요합니다.

