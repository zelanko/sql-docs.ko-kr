---
title: MSSQLSERVER_137 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2eaaadc4e1cc1f2f360fe3d45e2dea4c082b7b76
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915690"
---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
    
## <a name="details"></a>설명  
  
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
  
 EXECUTE 문 외부에서 선언된 변수를 참조하지 않도록 스크립트를 다시 작성하십시오. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20) ;  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>관련 항목  
 [EXECUTE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)   
 [SET 문&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
