---
title: SQL Server PowerShell 설치 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a90a30a0ae7fe09d49b1d42b577b13370c48c0de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775443"
---
# <a name="install-sql-server-powershell"></a>SQL Server PowerShell 설치
  사용자가 PowerShell 구성 요소가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 선택했지만 Windows PowerShell 2.0이 설치되지 않은 것으로 감지되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 중지됩니다. Windows 관리 프레임워크를 사용하여 PowerShell을 설치하고 설치 프로그램을 다시 실행해야 합니다.  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 지원 설치  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 Windows PowerShell에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원을 제공하는 소프트웨어를 설치해야 합니다. PowerShell 지원이 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 선택한 경우 Windows PowerShell 2.0이 설치되어 있는지 확인합니다. PowerShell 2.0이 있으면 설치 프로그램이 다음과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 구성 요소를 설치합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인. 이 스냅인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 두 가지 유형의 Windows PowerShell 지원을 구현하는 dll 파일입니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet 집합. Cmdlet은 특정 동작을 구현하는 명령입니다. 예를 들어 **Invoke-Sqlcmd** 는 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **유틸리티를 사용하여 실행할 수도 있는** 또는 XQuery 스크립트를 실행하고 **Invoke-PolicyEvaluation** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체가 정책 기반 관리 정책을 준수하는지 여부를 보고합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자입니다. 공급자를 사용하여 파일 시스템 경로와 유사한 경로로 표시되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색할 수 있습니다. 각 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체 모델의 클래스와 관련되어 있습니다. 클래스의 메서드 및 속성을 사용하여 개체에 대한 작업을 수행할 수 있습니다. 예를 들어 경로에서 databases 개체로 cd를 수행하는 경우 Microsoft.SqlServer.Managment.SMO.Database 클래스의 메서드와 속성을 사용하여 해당 데이터베이스를 관리할 수 있습니다.  
  
-   합니다 **sqlps** 로드 하기 위해 Windows PowerShell 2.0 세션으로 가져온 모듈을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅인입니다.  
  
-   사용 되지 않는 **sqlps** 유틸리티는 Windows PowerShell 2.0 세션을 시작 하 고 가져옵니다 합니다 **sqlps** 모듈입니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 은 개체 탐색기 트리에서 Windows PowerShell 세션을 시작하도록 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 Windows PowerShell 작업 단계를 지원합니다.  
  
 Windows PowerShell 2.0 설치 되지 않은, 또는 제거 된 경우 다음 지침에 따라 설치 해야 합니다 [Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214) 페이지입니다.  
  
 설치가 완료된 후 Windows PowerShell이 제거되면 Windows PowerShell의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능이 작동하지 않습니다. Windows 사용자는 Windows PowerShell을 제거할 수 있으며 일부 Windows 운영 체제 업그레이드 시 Windows PowerShell을 제거해야 할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 기능을 사용하려면 Windows 관리 프레임워크를 사용하여 PowerShell 2.0을 다시 설치해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
  
