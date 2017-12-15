---
title: "SQLPS 모듈 가져오기 | Microsoft 문서"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 360350a7b8e051bcab2e24df508ea97b742c52a4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="import-the-sqlps-module"></a>SQLPS 모듈 가져오기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] PowerShell에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 관리하는 데 권장되는 방법은 **sqlps** 모듈을 Windows PowerShell 환경으로 가져오는 것입니다. 이 모듈은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅인 및 관리 효율성 어셈블리를 로드하고 등록합니다.  Windows PowerShell 3.0부터 모듈은 명령에서 cmdlet 또는 모듈의 함수를 사용할 경우 자동으로 가져옵니다. 이 기능은 PSModulePath 환경 변수의 값에 포함된 디렉터리에서 모든 모듈에 대해 작동합니다.  자세한 내용은 [Importing a PowerShell Module](https://msdn.microsoft.com/library/dd878284(v=vs.85).aspx)(PowerShell 모듈 가져오기)을 참조하세요.
  
1.  **시작하기 전에:**  [보안](#Security)  
  
2.  **모듈을 로드하려면**  [sqlps 모듈 로드](#LoadSqlps)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 **sqlps** 모듈을 Windows PowerShell로 가져온 후 다음을 수행할 수 있습니다.  
  
-   대화형으로 Windows PowerShell 명령을 실행합니다.  
  
-   Windows PowerShell 스크립트 파일을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자 경로를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색합니다.  
  
-   Microsoft.SqlServer.Management.Smo 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 효율성 개체 모델을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 관리합니다.  
  
> [!NOTE]  
>  두 SQL Server cmdlet(**Encode-Sqlname** 및 **Decode-Sqlname**)의 이름에 사용되는 동사는 Windows PowerShell에 대해 승인된 동사와 일치하지 않습니다. 이로 인해 작동에는 영향을 주지 않지만 **sqlps** 모듈을 세션으로 가져올 때 Windows PowerShell에서 경고를 표시합니다.  
  
###  <a name="Security"></a> 보안  
 기본적으로 Windows PowerShell은 모든 Windows PowerShell 스크립트 실행을 방지하는 **제한됨**으로 설정된 스크립팅 실행 정책과 함께 실행됩니다. **sqlps** 모듈을 로드하려면 **Set-ExecutionPolicy** cmdlet을 사용하여 서명된 스크립트나 모든 스크립트를 실행하도록 설정할 수 있습니다. 신뢰할 수 있는 출처에서 제공하는 스크립트만 실행하고 적절한 NTFS 권한을 사용하여 모든 입력 및 출력 파일을 보호하십시오. Windows PowerShell 스크립트를 사용하도록 설정하는 방법은 [Windows PowerShell 스크립트 실행](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx)을 참조하십시오.  
  
##  <a name="LoadSqlps"></a> sqlps 모듈 로드  
 **Windows PowerShell에서 sqlps 모듈을 로드하려면**  
  
1.  **Set-ExecutionPolicy** cmdlet을 사용하여 적절한 스크립트 실행 정책을 설정합니다.  
  
2.  **Import-Module** cmdlet을 사용하여 sqlps 모듈을 가져옵니다. **Encode-Sqlname** 및 **Decode-Sqlname** 에 대한 경고를 억제하려면 **DisableNameChecking**매개 변수를 지정합니다.  
  
### <a name="example"></a>예제  
 이 예에서는 이름 확인을 해제한 상태로 **sqlps** 모듈을 로드합니다.  
  
```powershell 
# Import the SQL Server Module.    
Import-Module Sqlps -DisableNameChecking;

# To check whether the module is installed.
Get-Module -ListAvailable -Name Sqlps;
```  
  
> [!NOTE]  
>  **sqlps** 모듈이 경로에 있지 않은 경우 모듈의 위치를 변경하거나 스크립트에서 전체 경로를 사용합니다(경로의 폴더에 큰따옴표를 사용하면 공백이 생김). **sqlps** 모듈은 SQL Server 인스턴스에 대한 Tools\Powershell 폴더에 있습니다.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [&#91;맨 위로 이동&#93;]()  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [SQL Server PowerShell 공급자](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [데이터베이스 엔진 cmdlet 사용](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
 [PowerShell 모듈 설치](https://msdn.microsoft.com/library/dd878350(v=vs.85).aspx)  
 [Import-Module](https://technet.microsoft.com/library/hh849725.aspx)
  
  
