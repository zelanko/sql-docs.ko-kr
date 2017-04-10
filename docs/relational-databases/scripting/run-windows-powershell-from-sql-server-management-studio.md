---
title: "SQL Server Management Studio에서 Windows PowerShell 실행 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# SQL Server Management Studio에서 Windows PowerShell 실행
  **의** 개체 탐색기 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 Windows PowerShell 세션을 시작할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 Windows PowerShell을 시작하고, **sqlps** 모듈을 로드한 다음 경로 컨텍스트를 **개체 탐색기** 트리의 연결된 노드로 설정합니다.  
  
## 시작하기 전에  
 **개체 탐색기**에서 개체에 대해 PowerShell을 실행하도록 지정하면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인이 로드 및 등록된 Windows PowerShell 세션을 시작합니다. 세션 경로는 사용자가 개체 탐색기에서 마우스 오른쪽 단추로 클릭한 개체의 위치로 미리 설정됩니다. 예를 들어 개체 탐색기에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택하면 Windows PowerShell 경로가 다음과 같이 설정됩니다.  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## PowerShell 실행  
 **SQL Server Management Studio에서 PowerShell을 실행하려면**  
  
1.  **개체 탐색기**를 엽니다.  
  
2.  작업할 개체에 대한 노드로 이동합니다.  
  
3.  개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택합니다.  
  
## 사용 권한  
 PowerShell을 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 열 경우 관리자 권한으로 실행되지 않아 WMI에 대한 호출 등 일부 작업을 수행하지 못할 수 있습니다.  
  
## 참고 항목  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  