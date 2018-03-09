---
title: "MSSQLSERVER_137 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c242db0377a97305c26e35b53e165346af87815
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|137|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|P_SCALAR_VAR_NOTFOUND|  
|메시지 텍스트|스칼라 변수 "%.*ls"을(를) 선언해야 합니다.|  
  
## <a name="explanation"></a>설명  
이 오류는 SQL 스크립트에서 변수를 먼저 선언하지 않고 사용하는 경우에 발생합니다. 다음 예제에서는 **@mycol**이 선언되지 않았으므로 SET 및 SELECT 문에 대해 오류 137이 반환됩니다.  
  
SET @mycol = 'ContactName';  
  
SELECT @mycol;  
  
이 오류의 좀 더 복잡한 원인 중 하나로 EXECUTE 문 외부에서 선언된 변수를 사용하는 경우가 있습니다. 예를 들어 SELECT 문에 지정된 **@mycol** 변수는 SELECT 문에서 로컬로 사용되므로 EXECUTE 문 외부에 있습니다.  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20);  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>사용자 동작  
SQL 스크립트에서 변수를 사용하기 전에 해당 변수를 선언했는지 확인하십시오.  
  
EXECUTE 문 외부에서 선언된 변수를 참조하지 않도록 스크립트를 다시 작성하십시오. 예를 들어  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20) ;  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>참고 항목  
[EXECUTE&#40;Transact-SQL&#41;](~/t-sql/language-elements/execute-transact-sql.md)  
[SET 문&#40;Transact-SQL&#41;](~/t-sql/statements/set-statements-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](~/t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
