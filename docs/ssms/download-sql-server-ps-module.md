---
title: "SQL Server PowerShell 모듈을 다운로드 | Microsoft Docs"
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
- "sql server powershell을 다운로드 하 여 sql server powershell 설치"
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="download-sql-server-powershell-module"></a>SQL Server PowerShell 모듈을 다운로드
SQL Server Management Studio의 17.0 릴리스의 일부로 SQL Server PowerShell 모듈이 PowerShell 갤러리를 통해 제공 됩니다.  모듈은 더 이상 SSMS 설치 패키지에 포함 됩니다. PowerShell SSMS 17.0 버전과 새 버전을 사용 하려면 추가 단계로 SQL Server 모듈에서 컴퓨터에 설치 합니다.

Windows 관리 프레임 워크의 최신 버전을 설치 하는 방법에 대 한 설명서를 전체 및 PowerShell 모듈을 설치 하는 방법 일반적에서 확인할 수 있습니다는 [PowerShell 갤러리](https://www.powershellgallery.com/) 사이트입니다.

SQL Server 모듈을 설치 하려면 PowerShell 명령을 사용 합니다.

> Install-module-sql Server 이름 지정-CurrentUser 범위

이전 버전 컴퓨터에서 SQL Server PowerShell 모듈의 경우 제공 해야 할 수 있습니다는 "-AllowClobber" 매개 변수입니다.  

PowerShell 갤러리에 함께 제공 되는 SQL Server PowerShell 모듈의 버전 버전 관리를 지원 하 고 PowerShell 버전 5.0 이상이 필요 합니다.

