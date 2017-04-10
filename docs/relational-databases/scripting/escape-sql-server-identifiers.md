---
title: "SQL Server 식별자 이스케이프 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# SQL Server 식별자 이스케이프
  Windows PowerShell 역따옴표 이스케이프 문자(`)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 식별자에는 허용되고 Windows PowerShell 경로 이름에는 허용되지 않는 문자를 이스케이프 처리할 수도 있습니다. 하지만 이스케이프 처리되지 않는 문자도 있습니다. 예를 들어 Windows PowerShell에서 콜론 문자(:)는 이스케이프 처리할 수 없습니다. 해당 문자가 포함된 식별자는 인코딩해야 합니다. 인코딩은 모든 문자에 대해 작동하므로 이스케이프 처리보다 안정적입니다.  
  
## 시작하기 전 주의 사항  
 역따옴표 문자(`) 키는 일반적으로 키보드 왼쪽 위에서 ESC 키 아래에 있습니다.  
  
## 예  
 다음은 # 문자를 이스케이프 처리하는 예입니다.  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 다음은 (local)을 컴퓨터 이름으로 지정하는 경우 괄호를 이스케이프 처리하는 예입니다.  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## 참고 항목  
 [PowerShell의 SQL Server 식별자](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 공급자](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  