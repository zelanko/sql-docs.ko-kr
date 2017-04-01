---
title: "탭 완성 기능 관리(SQL Server PowerShell) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 탭 완성 기능 관리(SQL Server PowerShell)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인에 도입된 3개의 변수 (**$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems**, 및 **$SqlServerIncludeSystemObjects**)를 사용하여 Windows PowerShell 탭 완성 기능을 제어할 수 있습니다. 탭 완성 기능은 이름이 입력한 문자열로 시작하는 항목의 테이블을 반환하여 사용자 입력을 줄여 줍니다.  
  
## 시작하기 전 주의 사항  
 Windows PowerShell 탭 완성 기능을 사용하는 경우 특정 경로나 cmdlet 이름의 일부를 입력한 후 Tab 키를 누르면 입력한 이름과 일치하는 항목의 목록을 가져올 수 있습니다. 그런 다음 나머지 이름을 입력하지 않고 목록에서 원하는 항목을 선택할 수 있습니다.  
  
 개체가 많은 데이터베이스에서 작업 중인 경우에는 탭 완성 목록이 매우 커질 수 있습니다. 뷰와 같은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 유형에도 다수의 시스템 개체가 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅인에 도입된 3개의 시스템 변수를 사용하여 탭 완성 기능 및 **Get-ChildItem**에서 제공하는 정보의 양을 제어할 수 있습니다.  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 탭 완성 목록에 포함할 최대 개체 수를 지정합니다. 개체 수가 *n*보다 큰 경로 노드에서 Tab 키를 누르면 탭 완성 목록이 *n*개까지 표시됩니다. *n* 은 정수입니다. 0은 기본 설정이며 나열되는 개체 수에 제한이 없음을 의미합니다.  
  
 **$SqlServerMaximumChildItems =** *n*  
 **Get-ChildItem**에서 표시하는 최대 개체 수를 지정합니다. **Get-ChildItem**이 개체 수가 *n*보다 큰 경로 노드에서 실행되는 경우 목록은 *n*개까지 표시됩니다. *n* 은 정수입니다. 0은 기본 설정이며 나열되는 개체 수에 제한이 없음을 의미합니다.  
  
 **$SqlServerIncludeSystemObjects =** { **$True** | **$False** }  
 **$True**인 경우 탭 완성 기능 및 **Get-ChildItem**에서 시스템 개체를 표시하고, **$False**인 경우에는 시스템 개체를 표시하지 않습니다. 기본 설정은 **$False**입니다.  
  
## SQL Server 탭 완성 변수 설정  
 변수를 기본값이 아닌 다른 값으로 변경하려면 변수를 새 값으로 설정합니다.  
  
### 예제(PowerShell)  
 다음 예에서는 3개 변수를 모두 설정하고 해당 설정을 나열합니다.  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## 참고 항목  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  