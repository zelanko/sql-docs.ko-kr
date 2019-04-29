---
title: MSSQLSERVER_17065 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33dfe774838aa88dc0c68829ae0abe34f3f1dda9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62869757"
---
# <a name="mssqlserver17065"></a>MSSQLSERVER_17065
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17065|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLASSERT_BOTH|  
|메시지 텍스트|SQL Server Assertion: 파일: \<%s >, 줄 %d 어설션 = = '%s' %s입니다. 이 오류는 타이밍과 관련된 것일 수 있습니다. 문을 다시 실행한 후에도 이 오류가 지속되면 DBCC CHECKDB를 사용하여 데이터베이스의 구조적 무결성을 확인하거나 서버를 다시 시작하여 메모리 내부 데이터 구조가 손상되지 않도록 하십시오.|  
  
## <a name="explanation"></a>설명  
 이 오류는 일시적인 타이밍 관련 오류나 메모리 내부에 있거나 디스크에 있는 데이터의 손상으로 인해 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 예외를 발생시킨 문을 다시 실행합니다. 타이밍 관련 이벤트로 인해 발생한 오류는 되풀이되지 않을 수 있습니다. 문제가 지속되면 DBCC CHECKDB를 실행하여 디스크가 손상되었는지 확인합니다. 메모리 내부 데이터 구조가 손상되지 않았는지 확인하려면 서버를 다시 시작합니다.  
  
## <a name="see-also"></a>관련 항목  
 [DBCC CHECKDB&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
