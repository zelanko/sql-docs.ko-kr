---
title: SQLPS 모듈 가져오기 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: 9
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 8c20daf51270931609fb876b9a7035da343d19f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092466"
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
>  두 SQL Server cmdlet(`Encode-Sqlname` 및 `Decode-Sqlname`)의 이름에 사용되는 동사는 Windows PowerShell 2.0에 대해 승인된 동사와 일치하지 않습니다. 이 인해 작동에 영향을 주지 않지만 Windows PowerShell에서 경고를 표시 하면는 `sqlps` 모듈을 세션으로 가져올 합니다.  
  
###  <a name="Security"></a> 보안  
 기본적으로 Windows PowerShell은 모든 Windows PowerShell 스크립트 실행을 방지하는 **제한됨**으로 설정된 스크립팅 실행 정책과 함께 실행됩니다. `sqlps` 모듈을 로드하려면 `Set-ExecutionPolicy` cmdlet을 사용하여 서명된 스크립트나 기타 스크립트를 실행할 수 있도록 설정합니다. 신뢰할 수 있는 출처에서 제공하는 스크립트만 실행하고 적절한 NTFS 권한을 사용하여 모든 입력 및 출력 파일을 보호하십시오. Windows PowerShell 스크립트를 사용하도록 설정하는 방법은 [Windows PowerShell 스크립트 실행](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx)을 참조하십시오.  
  
##  <a name="LoadSqlps"></a> sqlps 모듈 로드  
 **Windows PowerShell에서 sqlps 모듈을 로드하려면**  
  
1.  사용 하 여는 `Set-ExecutionPolicy` cmdlet을 적절 한 스크립트 실행 정책을 설정 합니다.  
  
2.  사용 하 여는 `Import-Module` cmdlet sqlps 모듈을 가져옵니다. 지정 된 `DisableNameChecking` 에 대 한 경고를 억제 하려면 매개 변수 `Encode-Sqlname` 및 `Decode-Sqlname`합니다.  
  
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
  
  