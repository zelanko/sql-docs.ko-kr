---
title: MSSQLSERVER_17067 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17067 (Database Engine error)
ms.assetid: 32c1f0e8-db70-4836-95b2-8833be9e0ad1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2bd9a9d7e2c8b9d03c3fdaefd1364102cbd7ba56
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553698"
---
# <a name="mssqlserver_17067"></a>MSSQLSERVER_17067
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17067|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLASSERT_MESG|  
|메시지 텍스트|SQL Server 어설션: 파일: \<%s>, 줄 = %d %s. 이 오류는 타이밍과 관련된 것일 수 있습니다. 문을 다시 실행한 후에도 이 오류가 지속되면 DBCC CHECKDB를 사용하여 데이터베이스의 구조적 무결성을 확인하거나 서버를 다시 시작하여 메모리 내부 데이터 구조가 손상되지 않도록 하십시오.|  
  
## <a name="explanation"></a>설명  
 이 오류는 일시적인 타이밍 관련 오류나 메모리 내부에 있거나 디스크에 있는 데이터의 손상으로 인해 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 예외를 발생시킨 문을 다시 실행합니다. 타이밍 관련 이벤트로 인해 발생한 오류는 되풀이되지 않을 수 있습니다. 문제가 지속되면 DBCC CHECKDB를 실행하여 디스크가 손상되었는지 확인합니다. 메모리 내부 데이터 구조가 손상되지 않았는지 확인하려면 서버를 다시 시작합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DBCC CHECKDB&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
