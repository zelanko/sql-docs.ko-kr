---
title: SQL Server PowerShell 설치 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 26ddefde6223effd90d2130c40c28011de411802
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172240"
---
# <a name="install-sql-server-powershell"></a>SQL Server PowerShell 설치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 선택 검색 될 경우 설치 프로그램이 중지 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 했지만 Windows PowerShell 2.0 PowerShell 구성 요소를 포함 하는 기능이 설치 되어 있지 않습니다. Windows 관리 프레임워크를 사용하여 PowerShell을 설치하고 설치 프로그램을 다시 실행해야 합니다.  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 지원 설치  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 Windows PowerShell에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원을 제공하는 소프트웨어를 설치해야 합니다. 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 요구 하는 기능 지원, 설치 프로그램에서 Windows PowerShell 2.0이 설치 되어 있는지 확인 합니다. PowerShell 2.0이 있으면 설치 프로그램 다음 설치 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 구성 요소:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인. 이 스냅인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 두 가지 유형의 Windows PowerShell 지원을 구현하는 dll 파일입니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet 집합. Cmdlet은 특정 동작을 구현하는 명령입니다. 예를 들어 **Invoke-Sqlcmd** 는 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **유틸리티를 사용하여 실행할 수도 있는** 또는 XQuery 스크립트를 실행하고 **Invoke-PolicyEvaluation** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체가 정책 기반 관리 정책을 준수하는지 여부를 보고합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자입니다. 공급자를 사용하여 파일 시스템 경로와 유사한 경로로 표시되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색할 수 있습니다. 각 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체 모델의 클래스와 관련되어 있습니다. 클래스의 메서드 및 속성을 사용하여 개체에 대한 작업을 수행할 수 있습니다. 예를 들어 경로에서 databases 개체로 cd를 수행하는 경우 Microsoft.SqlServer.Managment.SMO.Database 클래스의 메서드와 속성을 사용하여 해당 데이터베이스를 관리할 수 있습니다.  
  
-   **sqlps** 로드 하기 위해 Windows PowerShell 2.0 세션으로 가져온 모듈에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅인.  
  
-   사용 되지 않는 **sqlps** Windows PowerShell 2.0 세션을 시작 하 여 가져오는 유틸리티는 **sqlps** 모듈입니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 은 개체 탐색기 트리에서 Windows PowerShell 세션을 시작하도록 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 Windows PowerShell 작업 단계를 지원합니다.  
  
 Windows PowerShell 2.0 설치 되지 않은 제거 된 경우의 지침에 따라 설치 해야는 [Windows 관리 프레임 워크](http://go.microsoft.com/fwlink/?LinkId=186214) 페이지.  
  
 설치가 완료 되 면 Windows PowerShell이 제거 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능이 Windows PowerShell에서는 작동 하지 않습니다. Windows 사용자는 Windows PowerShell을 제거할 수 있으며 일부 Windows 운영 체제 업그레이드 시 Windows PowerShell을 제거해야 할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 기능을 사용하려면 Windows 관리 프레임워크를 사용하여 PowerShell 2.0을 다시 설치해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
  