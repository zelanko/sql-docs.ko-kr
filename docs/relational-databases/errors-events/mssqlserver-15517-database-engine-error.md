---
title: MSSQLSERVER_15517 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8b08e71c58edf096a3ba07f12fdaa2972b1e3b32
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver15517"></a>MSSQLSERVER_15517
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|15517|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_CANNOTEXECUTEASUSER|  
|메시지 텍스트|보안 주체 "*principal*"이(가) 없거나 이 유형의 보안 주체를 가장할 수 없거나 사용 권한이 없기 때문에 데이터베이스 보안 주체로 실행할 수 없습니다.|  
  
## <a name="user-action"></a>사용자 동작  
기존 보안 주체의 이름을 사용하거나 해당 보안 주체에 대한 IMPERSONATE 권한을 가져옵니다.  
  
15517은 원래 데이터베이스 소유자 이외의 다른 사용자가 데이터베이스 연결 및 복원을 수행한 후에 발생할 수 있습니다. 이 오류를 해결하려면 다음 명령을 실행해서 db_owner를 서버의 로그인 계정으로 변경합니다.  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>참고 항목  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
