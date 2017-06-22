---
title: "데이터베이스 엔진 오류 이해 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [SQL Server], about errors
- errors [SQL Server], Database Engine
- errors [SQL Server]
- Database Engine [SQL Server], errors
ms.assetid: ddaca9d3-956f-46a5-8cd3-a7a15ec75878
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fab32eee7823d80a531503a88b9a58dff06c5b89
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="understanding-database-engine-errors"></a>데이터베이스 엔진 오류 이해
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 발생한 오류에는 다음 표에 설명된 것과 같은 특성이 있습니다.  
  
|Attribute|설명|  
|---------------|-----------------|  
|오류 번호|모든 오류 메시지에는 고유한 오류 번호가 있습니다.|  
|오류 메시지 문자열|오류 메시지에는 오류 발생 원인에 대한 진단 정보가 포함됩니다. 많은 오류 메시지에는 오류를 발생시킨 개체 이름과 같은 정보가 포함된 대체 변수가 있습니다.|  
|Severity|오류의 심각도를 나타냅니다. 심각도가 낮은 오류(심각도가 1 또는 2인 경우)는 정보 메시지이거나 하위 수준 경고이며 심각도가 높은 오류는 가능한 빨리 해결해야 할 문제를 가리킵니다. 심각도에 대한 자세한 내용은 [데이터베이스 엔진 오류 심각도](../../relational-databases/errors-events/database-engine-error-severities.md)를 참조하세요.|  
|State|일부 오류 메시지는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]코드의 여러 곳에서 발생할 수 있습니다. 예를 들어 1105 오류는 여러 가지 다른 조건에서 발생합니다. 오류를 발생시키는 각각의 특정 조건마다 고유한 상태 코드를 할당합니다.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료와 같이 알려진 문제에 대한 정보를 포함하는 데이터베이스를 확인하는 경우 상태 번호를 사용하여 기록된 문제가 실제로 발생한 오류와 동일한지 여부를 확인할 수 있습니다. 예를 들어 기술 자료 문서에서 상태가 2인 1105 오류에 대해 설명하는데 실제로 발생한 1105 오류 메시지의 상태가 3인 경우 이 오류가 기술 자료 문서에 보고된 것과 다른 원인에서 비롯되었을 가능성이 높습니다.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 엔지니어도 오류의 상태 코드를 사용하여 원본 코드에서 해당 오류 코드가 발생한 위치를 찾을 수 있습니다. 이 정보는 문제 진단에 도움이 될 수 있습니다.|  
|프로시저 이름|오류가 발생한 저장 프로시저 또는 트리거의 이름입니다.|  
|줄 번호|일괄 처리, 저장 프로시저, 트리거 또는 함수에서 오류를 발생시킨 문을 가리킵니다.|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 모든 시스템 및 사용자 정의 오류 메시지는 **sys.messages** 카탈로그 뷰에 포함되어 있습니다. RAISERROR 문을 사용하여 응용 프로그램에 사용자 정의 오류를 반환할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **SQLClient** 네임스페이스, ADO(ActiveX Data Objects), OLE DB 및 ODBC(Open Database Connectivity)를 비롯한 모든 데이터베이스 API는 기본 오류 특성을 보고합니다. 이 정보에는 오류 번호와 메시지 문자열이 포함됩니다. 그러나 일부 API는 일부 오류 특성을 보고하지 않을 수 있습니다.  
  
 TRY...CATCH 구문의 TRY 블록 범위 내에서 발생하는 오류에 대한 정보는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드의 관련 CATCH 블록 범위 내에서 ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY 및 ERROR_STATE와 같은 함수를 사용하여 얻을 수 있습니다. 자세한 내용은 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 영문( `sys.messages` ) 텍스트가 포함된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 모든 시스템 및 사용자 정의 오류 메시지 목록을 반환하기 위해`1033`카탈로그 뷰를 쿼리합니다.  
  
```  
SELECT  
    message_id,  
    language_id,  
    severity,  
    is_event_logged,  
    text  
  FROM sys.messages  
  WHERE language_id = 1033;  
```  
  
 자세한 내용은 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE&#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)  
  
  
