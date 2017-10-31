---
title: "MSSQLSERVER_41333 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 72f5461f4e60b7e4c5cb53df75906d1aae0a07a5
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41333|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|CROSS_CONTAINER_ISOLATION_FAILURE|  
|메시지 텍스트|RepeatableRead 트랜잭션, Serializable 트랜잭션 및 RepeatableRead 또는 Serializable 격리 상태에서 메모리에 최적화되지 않은 테이블에 액세스하는 트랜잭션은 스냅숏 격리 하에 메모리 액세스에 최적화된 테이블 및 고유하게 컴파일된 저장 프로시저에 액세스해야 합니다.|  
  
## <a name="explanation"></a>설명  
디스크 기반 트랜잭션과 XTP 트랜잭션 간에는 높은 격리 수준의 사용자에 대한 제한 사항이 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
메모리 액세스에 최적화된 테이블(및 고유하게 컴파일된 프로시저) 및 디스크 기반 테이블에서는 높은 수준의 격리 작업을 시도하지 마십시오.  
  
자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

