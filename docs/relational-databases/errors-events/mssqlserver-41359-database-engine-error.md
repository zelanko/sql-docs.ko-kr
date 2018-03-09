---
title: "MSSQLSERVER_41359 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c233a31bd2f0c17ef8081db3a42e4be89b753092
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver41359"></a>MSSQLSERVER_41359
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41359|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|메시지 텍스트|데이터베이스 옵션 READ_COMMITTED_SNAPSHOT이 ON으로 설정된 경우 READ COMMITTED 격리 수준을 사용하여 메모리 액세스에 최적화된 테이블에 액세스하는 쿼리가 디스크 기반 테이블에 액세스할 수 없습니다. WITH (SNAPSHOT) 같은 테이블 힌트를 사용하여 메모리 액세스에 최적화된 테이블에 대해 지원되는 격리 수준을 제공합니다.|  
  
## <a name="explanation"></a>설명  
READ_COMMITTED_SNAPSHOT이 ON으로 설정된 데이터베이스는 메모리 최적화 테이블과 디스크 기반 테이블에 모두 액세스하는 트랜잭션을 지원하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
READ_COMMITTED_SNAPSHOT을 OFF로 설정하거나 WITH (SNAPSHOT) 같은 테이블 수준 힌트를 사용하여 메모리 최적화 테이블에 대해 지원되는 격리 수준을 제공합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
