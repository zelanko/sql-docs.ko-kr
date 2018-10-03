---
title: SQLPS 모듈 가져오기 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e687fd8c7fcd7c21f8aac9b546492a8f9bd4a644
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077243"
---
# <a name="import-the-sqlps-module"></a>SQLPS 모듈 가져오기
  PowerShell에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 관리하는 데 권장되는 방법은 `sqlps` 모듈을 Windows PowerShell 2.0 환경으로 가져오는 것입니다. 이 모듈은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스냅인 및 관리 효율성 어셈블리를 로드하고 등록합니다.  
  
1.  **시작하기 전에:**  [보안](#Security)  
  
2.  **모듈을 로드하려면**  [sqlps 모듈 로드](#LoadSqlps)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 `sqlps` 모듈을 Windows PowerShell로 가져온 후 다음을 수행할 수 있습니다.  
  
-   대화형으로 Windows PowerShell 명령을 실행합니다.  
  
-   Windows PowerShell 스크립트 파일을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자 경로를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색합니다.  
  
-   Microsoft.SqlServer.Management.Smo 같은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리 효율성 개체 모델을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체를 관리합니다.  
  
> [!NOTE]  
>  두 SQL Server cmdlet(`Encode-Sqlname` 및 `Decode-Sqlname`)의 이름에 사용되는 동사는 Windows PowerShell 2.0에 대해 승인된 동사와 일치하지 않습니다. 이 해당 작업에 영향을 주지 않지만 Windows PowerShell에서 경고를 때는 `sqlps` 세션에 모듈을 가져옵니다.  
  
###  <a name="Security"></a> 보안  
 기본적으로 Windows PowerShell은 모든 Windows PowerShell 스크립트 실행을 방지하는 **제한됨**으로 설정된 스크립팅 실행 정책과 함께 실행됩니다. `sqlps` 모듈을 로드하려면 `Set-ExecutionPolicy` cmdlet을 사용하여 서명된 스크립트나 기타 스크립트를 실행할 수 있도록 설정합니다. 신뢰할 수 있는 출처에서 제공하는 스크립트만 실행하고 적절한 NTFS 권한을 사용하여 모든 입력 및 출력 파일을 보호하십시오. Windows PowerShell 스크립트를 사용하도록 설정하는 방법은 [Windows PowerShell 스크립트 실행](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx)을 참조하십시오.  
  
##  <a name="LoadSqlps"></a> sqlps 모듈 로드  
 **Windows PowerShell에서 sqlps 모듈을 로드하려면**  
  
1.  사용 된 `Set-ExecutionPolicy` 적절 한 스크립트 실행 정책을 설정 하는 cmdlet입니다.  
  
2.  사용 된 `Import-Module` sqlps 모듈을 가져오기 위한 cmdlet입니다. 지정 된 `DisableNameChecking` 에 대 한 경고를 표시 하지 않으려는 경우 매개 변수 `Encode-Sqlname` 및 `Decode-Sqlname`합니다.  
  
### <a name="example-powershell"></a>예제(PowerShell)  
 이 예에서는 이름 확인을 해제한 상태로 `sqlps` 모듈을 로드합니다.  
  
```  
## Import the SQL Server Module.  
  
Import-Module “sqlps” -DisableNameChecking  
  
```  
  

  
## <a name="see-also"></a>관련 항목  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)   
 [데이터베이스 엔진 cmdlet 사용](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
