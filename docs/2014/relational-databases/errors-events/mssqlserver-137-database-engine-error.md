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
ms.openlocfilehash: 72e0b54f26c323c16efa8c67aea1c325e8ddf72d
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552290"
---
# <a name="mssqlserver_137"></a>MSSQLSERVER_137
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|137|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|P_SCALAR_VAR_NOTFOUND|  
|메시지 텍스트|스칼라 변수 "%.*ls"을(를) 선언해야 합니다.|  
  
## <a name="explanation"></a>설명  
 이 오류는 SQL 스크립트에서 변수를 먼저 선언하지 않고 사용하는 경우에 발생합니다. 다음 예에서는가 선언 되지 않았으므로 SET 및 SELECT 문에 대해 모두 오류 137을 반환 합니다 **@mycol** .  
  
 SET @mycol = 'ContactName';  
  
 SELECT @mycol;  
  
 이 오류의 좀 더 복잡한 원인 중 하나로 EXECUTE 문 외부에서 선언된 변수를 사용하는 경우가 있습니다. 예를 들어 **@mycol** select 문에 지정 된 변수는 select 문에 로컬인 것 이므로 EXECUTE 문 외부에 있습니다.  
  
 USE AdventureWorks2012;  
  
 이동  
  
 DECLARE @mycol nvarchar(20);  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>사용자 동작  
 SQL 스크립트에서 변수를 사용하기 전에 해당 변수를 선언했는지 확인하십시오.  
  
 EXECUTE 문 외부에서 선언된 변수를 참조하지 않도록 스크립트를 다시 작성하십시오. 예를 들면 다음과 같습니다.  
  
 USE AdventureWorks2012;  
  
 이동  
  
 DECLARE @mycol nvarchar(20) ;  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>참고 항목  
 [EXECUTE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)   
 [SET 문&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
