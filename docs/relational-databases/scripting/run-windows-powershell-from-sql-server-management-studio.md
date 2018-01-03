---
title: "SQL Server Management Studio에서 Windows PowerShell 실행 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f5ed1e815f1a98d791d7cf7d95ce233de15c3d02
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio에서 Windows PowerShell 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **개체 탐색기**에서 Windows PowerShell 세션을 시작할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 Windows PowerShell을 시작하고, **sqlps** 모듈을 로드한 다음 경로 컨텍스트를 **개체 탐색기** 트리의 연결된 노드로 설정합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 **개체 탐색기**에서 개체에 대해 PowerShell을 실행하도록 지정하면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인이 로드 및 등록된 Windows PowerShell 세션을 시작합니다. 세션 경로는 사용자가 개체 탐색기에서 마우스 오른쪽 단추로 클릭한 개체의 위치로 미리 설정됩니다. 예를 들어 개체 탐색기에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택하면 Windows PowerShell 경로가 다음과 같이 설정됩니다.  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>PowerShell 실행  
 **SQL Server Management Studio에서 PowerShell을 실행하려면**  
  
1.  **개체 탐색기**를 엽니다.  
  
2.  작업할 개체에 대한 노드로 이동합니다.  
  
3.  개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택합니다.  
  
## <a name="permissions"></a>사용 권한  
 PowerShell을 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 열 경우 관리자 권한으로 실행되지 않아 WMI에 대한 호출 등 일부 작업을 수행하지 못할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
