---
title: MSSQLSERVER_41333 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab94977bcd3bf5a9b0b26ac7be76cb67d58e0755
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913989"
---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41333|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|CROSS_CONTAINER_ISOLATION_FAILURE|  
|메시지 텍스트|트랜잭션은은 메모리 최적화 테이블에 액세스 해야 하 고 스냅숏 격리에서 저장된 프로시저를 고유 하 게 컴파일된: RepeatableRead 트랜잭션, Serializable 트랜잭션 및 RepeatableRead 또는 Serializable 격리 상태에서 액세스에 최적화 된 메모리 되지 않은 테이블에 액세스 하는 트랜잭션.|  
  
## <a name="explanation"></a>설명  
 디스크 기반 트랜잭션과 XTP 트랜잭션 간에는 높은 격리 수준의 사용자에 대한 제한 사항이 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 메모리 최적화 테이블(및 고유하게 컴파일된 프로시저) 및 디스크 기반 테이블에서는 높은 수준의 격리 작업을 시도하지 마세요.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
