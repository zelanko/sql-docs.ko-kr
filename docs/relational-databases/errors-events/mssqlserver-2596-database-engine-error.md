---
title: MSSQLSERVER_2596 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13db903ae2531ae6cbc69c334f458a357b4f73e4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2596|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|메시지 텍스트|복구 문이 처리되지 않았습니다. 데이터베이스는 읽기 전용 모드일 수 없습니다.|  
  
## <a name="explanation"></a>설명  
이 메시지는 데이터베이스가 읽기 전용 모드임을 나타냅니다. 데이터베이스가 읽기 전용 모드인 경우 복구할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
ALTER DATABASE를 사용하여 데이터베이스를 읽기/쓰기 권한으로 설정한 다음 DBCC 명령을 다시 실행하십시오.  
  
## <a name="see-also"></a>참고 항목  
[ALTER DATABASE&#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  
