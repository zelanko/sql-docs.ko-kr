---
title: SQL Server PowerShell 설치 | Microsoft Docs
description: 이 문서에서는 PowerShell 지원이 필요한 SQL Server 기능을 선택할 경우 설치 프로그램에서 설치하는 SQL Server PowerShell 구성 요소에 대해 설명합니다.
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 4731394c13be32cbaa2529af9638820922720ce3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440274"
---
# <a name="install-sql-server-powershell"></a>SQL Server PowerShell 설치
[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 PowerShell 구성 요소를 자동으로 구성합니다.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 Windows PowerShell에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원을 제공하는 소프트웨어를 설치해야 합니다. PowerShell 지원이 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 선택한 경우 설치 프로그램에서 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 구성 요소를 설치합니다.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인. 이 스냅인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 두 가지 유형의 Windows PowerShell 지원을 구현하는 dll 파일입니다.  
  
  - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet 집합. Cmdlet은 특정 동작을 구현하는 명령입니다. 예를 들어 **Invoke-Sqlcmd** 는 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **유틸리티를 사용하여 실행할 수도 있는** 또는 XQuery 스크립트를 실행하고 **Invoke-PolicyEvaluation** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체가 정책 기반 관리 정책을 준수하는지 여부를 보고합니다.  
  
  - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자입니다. 공급자를 사용하여 파일 시스템 경로와 유사한 경로로 표시되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색할 수 있습니다. 각 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체 모델의 클래스와 관련되어 있습니다. 클래스의 메서드 및 속성을 사용하여 개체에 대한 작업을 수행할 수 있습니다. 예를 들어 경로에서 databases 개체로 cd를 수행하는 경우 Microsoft.SqlServer.Managment.SMO.Database 클래스의 메서드와 속성을 사용하여 해당 데이터베이스를 관리할 수 있습니다.  
 
- **스냅인을 로드하기 위해 Windows PowerShell 세션으로 가져온** sqlps [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모듈  
 
- [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 은 개체 탐색기 트리에서 Windows PowerShell 세션을 시작하도록 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 Windows PowerShell 작업 단계를 지원합니다.  
  
Windows Server 2012 이상 및 Windows 8 이상 버전에는 PowerShell이 설치 및 구성되어 있습니다. Windows PowerShell 설치에 대한 자세한 내용은 [Windows PowerShell 설치](/powershell/scripting/install/installing-windows-powershell)를 참조하세요.  

자세한 내용은 다음을 참조하세요.   

- [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
