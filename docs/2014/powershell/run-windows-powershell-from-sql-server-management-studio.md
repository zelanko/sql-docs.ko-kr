---
title: SQL Server Management Studio에서 Windows PowerShell 실행 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6d71f1158ef73b84e5b04dcc9a1970bfd7dce35
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783098"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio에서 Windows PowerShell 실행
  **의** 개체 탐색기 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 Windows PowerShell 세션을 시작할 수 있습니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]Windows PowerShell을 시작 하 고 `sqlps` 모듈을 로드 한 다음 경로 컨텍스트를 **개체 탐색기** 트리의 연결 된 노드로 설정 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
 **개체 탐색기**에서 개체에 대해 powershell을 실행 하도록 지정 하면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] powershell 스냅인이 로드 및 등록 된 Windows powershell 세션을 시작 합니다. 세션 경로는 사용자가 개체 탐색기에서 마우스 오른쪽 단추로 클릭한 개체의 위치로 미리 설정됩니다. 예를 들어 개체 탐색기에서 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택하면 Windows PowerShell 경로가 다음과 같이 설정됩니다.  
  
```
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="to-run-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio에서 PowerShell을 실행하려면 
  
1.  **개체 탐색기**를 엽니다.  
  
2.  작업할 개체에 대한 노드로 이동합니다.  
  
3.  개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택합니다.  
  
## <a name="permissions"></a>사용 권한  
 PowerShell을 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 열 경우 관리자 권한으로 실행되지 않아 WMI에 대한 호출 등 일부 작업을 수행하지 못할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell](sql-server-powershell.md)  
