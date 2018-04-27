---
title: SQL Server PowerShell 경로 탐색 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: powershell
ms.service: ''
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d68aca48-d161-45ed-9f4f-14122ed30218
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b438b9695dfedff07fe67f41fc120b9e53e5c161
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="navigate-sql-server-powershell-paths"></a>SQL Server PowerShell 경로 탐색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssDE](../includes/ssde-md.md)] PowerShell 공급자는 SQL Server 인스턴스의 개체를 파일 경로와 비슷한 구조로 표시합니다. Windows PowerShell cmdlet을 사용하여 공급자 경로를 탐색하고 사용자 지정 드라이브를 만들어 입력해야 하는 경로를 단축할 수 있습니다.  

> [!NOTE]
> SQL Server PowerShell 모듈은 **SqlServer**와 **SQLPS**의 두 가지가 있습니다. **SQLPS** 모듈은 (이전 버전과의 호환성을 위해) SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다. **SqlServer** 모듈은 **SQLPS**에 업데이트된 버전의 cmdlet이 포함되어 있으며, 최신 SQL 기능을 지원하는 새로운 cmdlet도 포함되어 있습니다.  
> 이전 버전의 **SqlServer** 모듈은 SSMS(SQL Server Management Studio)에 *포함되었습니다*(SSMS 16.x 버전만 해당). SSMS 17.0 이상이 포함된 PowerShell을 사용하려면 PowerShell 갤러리에서 **SqlServer** 모듈을 설치해야 합니다.
> **SqlServer** 모듈을 설치하려면 [SQL Server PowerShell 설치](download-sql-server-ps-module.md)를 참조하세요.
  
Windows PowerShell은 cmdlet을 구현하여 PowerShell 공급자가 지원하는 개체의 계층 구조를 보여주는 경로 구조를 탐색합니다. 경로의 노드를 탐색한 후 다른 cmdlet을 사용하여 현재 개체에 대한 기본 작업을 수행할 수 있습니다. cmdlet은 자주 사용되므로 간단한 정규 별칭을 가지고 있습니다. 또한 cmdlet을 유사한 명령 프롬프트 명령에 매핑하는 별칭 집합과 UNIX 셸 명령에 대한 별칭 집합도 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자는 다음 테이블과 같이 공급자 cmdlet의 하위 집합을 구현합니다.  
  
|cmdlet|정규 별칭|cmd 별칭|UNIX 셸 별칭|Description|  
|------------|---------------------|---------------|----------------------|-----------------|  
|**Get-Location**|**gl**|**pwd**|**pwd**|현재 노드를 가져옵니다.|  
|**Set-Location**|**sl**|**cd, chdir**|**cd, chdir**|현재 노드를 변경합니다.|  
|**Get-ChildItem**|**gci**|**dir**|**ls**|현재 노드에 저장된 개체를 나열합니다.|  
|**Get-Item**|**gi**|||현재 항목의 속성을 반환합니다.|  
|**Rename-Item**|**rni**|**rn**|**ren**|개체 이름을 바꿉니다.|  
|**Remove-Item**|**ri**|**del, rd**|**rm, rmdir**|개체를 제거합니다.|  
  
> [!IMPORTANT]  
>  일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 식별자(개체 이름)의 경우 Windows PowerShell에서 지원하지 않는 문자가 경로 이름에 포함되어 있습니다. 이러한 문자가 포함된 이름을 사용하는 방법은 [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md)을 참조하십시오.  
  
### <a name="sql-server-information-returned-by-get-childitem"></a>Get-ChildItem이 반환하는 SQL Server 정보  
 **Get-ChildItem** 또는 **dir** 및 **ls** 별칭에서 반환하는 정보는 SQLSERVER: 경로에서의 현재 위치에 따라 결정됩니다.  
  
|경로 위치|Get-ChildItem 결과|  
|-------------------|----------------------------|  
|SQLSERVER:\SQL|로컬 컴퓨터의 이름을 반환합니다. SMO 또는 WMI를 사용하여 다른 컴퓨터에 있는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스에 연결한 경우에는 해당 컴퓨터도 나열됩니다.|  
|SQLSERVER:\SQL\\*ComputerName*|컴퓨터에 있는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스의 목록입니다.|  
|SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*|Endpoints, Certificates 및 Databases와 같은 인스턴스의 최상위 개체 유형 목록입니다.|  
|Databases와 같은 개체 클래스 노드|데이터베이스(예: master, model, AdventureWorks20008R2) 목록과 같은 해당 유형의 개체 목록입니다.|  
|AdventureWorks2012와 같은 개체 이름 노드|개체 내에 포함된 개체 유형 목록입니다. 예를 들어 데이터베이스는 테이블 및 뷰와 같은 개체 유형을 나열합니다.|  
  
 기본적으로 **Get-ChildItem** 은 시스템 개체를 나열하지 않습니다. *Force* 매개 변수를 사용하여 **sys** 스키마의 개체와 같은 시스템 개체를 볼 수 있습니다.  
  
### <a name="custom-drives"></a>사용자 지정 드라이브  
 Windows PowerShell을 통해 사용자는 PowerShell 드라이브라고 하는 가상 드라이브를 정의할 수 있습니다. 이러한 가상 드라이브는 경로 문의 시작 노드로 매핑되며 일반적으로 자주 형식화되는 경로를 줄이는 데 사용됩니다. SQLSERVER: 경로가 길어지면 Windows PowerShell 창에서 공간을 차지하고 많은 텍스트를 입력해야 할 수 있습니다. 특정 경로 노드에서 많은 작업을 수행하려는 경우 해당 노드에 매핑되는 사용자 지정 Windows PowerShell 드라이브를 정의할 수 있습니다.  
  
## <a name="use-powershell-cmdlet-aliases"></a>PowerShell cmdlet 별칭 사용  
 **cmdlet 별칭 사용**  
  
-   전체 cmdlet 이름을 입력하는 대신 익숙한 명령 프롬프트 명령에 매핑되는 별칭이나 단축 별칭을 입력합니다.  
  
### <a name="alias-example-powershell"></a>별칭 예(PowerShell)  
 예를 들어 SQLSERVER:\SQL 폴더로 이동하고 해당 폴더의 자식 항목 목록을 요청하여 사용 가능한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 목록을 검색하려면 다음과 같은 cmdlet 또는 별칭의 집합 중 하나를 사용하면 됩니다.  
  
```  
## Shows using the full cmdet name.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## Shows using canonical aliases.  
sl SQLSERVER:\SQL  
gci  
  
## Shows using command prompt aliases.  
cd SQLSERVER:\SQL  
dir  
  
## Shows using Unix shell aliases.  
cd SQLSERVER:\SQL  
ls  
```  
  
## <a name="use-get-childitem"></a>Get-ChildItem 사용  
 **Get-Childitem을 사용하여 정보 반환**  
  
1.  자식 요소의 목록을 원하는 노드로 이동합니다.  
  
2.  Get-childitem을 실행하여 목록 가져옵니다.  
  
### <a name="get-childitem-example-powershell"></a>Get-childitem 예(PowerShell)  
 다음 예에서는 SQL Server 공급자 경로의 각 노드에 대해 Get-ChildItem이 반환하는 정보에 대해 설명합니다.  
  
```  
## Return the current computer and any computer  
## to which you have made a SQL or WMI connection.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## List the instances of the Database Engine on the local computer.  
  
Set-Location SQLSERVER:\SQL\localhost  
Get-ChildItem  
  
## Lists the categories of objects available in the  
## default instance on the local computer.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT  
Get-ChildItem  
  
## Lists the databases from the local default instance.  
## The force parameter is used to include the system databases.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-ChildItem -force  
```  
  
## <a name="create-a-custom-drive"></a>사용자 지정 드라이브 만들기  
 **사용자 지정 드라이브 만들기 및 사용**  
  
1.  **New-PSDrive** 를 사용하여 사용자 지정 드라이브를 정의할 수 있습니다. **Root** 매개 변수를 사용하여 사용자 지정 드라이브 이름에 표시되는 경로를 지정할 수 있습니다.  
  
2.  경로 탐색 cmdlet(예: **Set-Location**)에서 사용자 지정 드라이브 이름을 참조합니다.  
  
### <a name="custom-drive-example-powershell"></a>사용자 지정 드라이브 예(PowerShell)  
 이 예에서는 AdventureWorks2012 예제 데이터베이스의 배포된 복사본에 대해 노드에 매핑되는 AWDB라는 가상 드라이브를 만듭니다. 그런 다음 가상 드라이브를 사용하여 데이터베이스에서 테이블을 탐색합니다.  
  
```  
## Create a new virtual drive.  
New-PSDrive -Name AWDB -Root SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
  
## Use AWDB: to navigate to a specific table.  
Set-Location AWDB:\Tables\Purchasing.Vendor  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell 경로 작업](work-with-sql-server-powershell-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
