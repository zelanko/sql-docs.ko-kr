---
title: MSSQLSERVER_41399 | Microsoft 문서
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
- 41399 (Database Engine error)
ms.assetid: 5e5acb07-16ca-4329-8210-cd2bab0c904f
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e18e954e19b87656cce1dbf6099b96cc5701c30e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver41399"></a>MSSQLSERVER_41399
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41399|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|MAX_SORT_ROW_WIDTH_EXCEEDED|  
|메시지 텍스트|정렬 작업이 너무 복잡합니다. 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
조인 및 집계 작업의 결과 정렬 작업은 정렬 버퍼의 행 크기를 늘려 정렬 작업의 복잡성을 가중시킵니다. 이 오류는 행 크기가 고유하게 컴파일된 저장 프로시저의 정렬 연산자에 지원되는 최대 크기보다 크다는 것을 의미합니다. 정렬 버퍼의 행 크기는 전적으로 조인 수 및 집계 함수의 수와 유형에 따라 결정됩니다. 기본 테이블의 행 크기는 버퍼의 행 크기에 영향을 주지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
조인이나 집계 함수를 제거하여 쿼리를 단순화하십시오.  
  
## <a name="see-also"></a>참고 항목  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
