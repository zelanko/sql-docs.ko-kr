---
title: SQL Server 식별자 이스케이프 | Microsoft 문서
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
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dda716b6d61a9ec54a61b5a910407810fffd12d5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="escape-sql-server-identifiers"></a>SQL Server 식별자 이스케이프
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

역따옴표 이스케이프 문자(`)를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구분 식별자에는 허용되고 Windows PowerShell 경로 이름에는 허용되지 않는 문자를 이스케이프 처리할 수도 있습니다. 하지만 이스케이프 처리되지 않는 문자도 있습니다. 예를 들어 Windows PowerShell에서 콜론 문자(:)는 이스케이프 처리할 수 없습니다. 해당 문자가 포함된 식별자는 인코딩해야 합니다. 인코딩은 모든 문자에 대해 작동하므로 이스케이프 처리보다 안정적입니다.  

> [!NOTE]
> SQL Server PowerShell 모듈은 **SqlServer**와 **SQLPS**의 두 가지가 있습니다. **SQLPS** 모듈은 (이전 버전과의 호환성을 위해) SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다. **SqlServer** 모듈은 **SQLPS**에 업데이트된 버전의 cmdlet이 포함되어 있으며, 최신 SQL 기능을 지원하는 새로운 cmdlet도 포함되어 있습니다.
> 이전 버전의 **SqlServer** 모듈은 SSMS(SQL Server Management Studio)에 *포함되었습니다*(SSMS 16.x 버전만 해당). SSMS 17.0 이상이 포함된 PowerShell을 사용하려면 PowerShell 갤러리에서 **SqlServer** 모듈을 설치해야 합니다.
> **SqlServer** 모듈을 설치하려면 [SQL Server PowerShell 설치](download-sql-server-ps-module.md)를 참조하세요.

역따옴표 문자(`) 키는 일반적으로 키보드 왼쪽 위에서 ESC 키 아래에 있습니다.  
  
## <a name="examples"></a>예  
 다음은 # 문자를 이스케이프 처리하는 예입니다.  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 다음은 (local)을 컴퓨터 이름으로 지정하는 경우 괄호를 이스케이프 처리하는 예입니다.  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## <a name="see-also"></a>참고 항목  
 [PowerShell의 SQL Server 식별자](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
