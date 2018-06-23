---
title: MSSQLSERVER_41359 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6fc668ebab849134cc7e6fb4099c03588f1ad1e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184069"
---
# <a name="mssqlserver41359"></a>MSSQLSERVER_41359
    
## <a name="details"></a>설명  
  
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
 READ_COMMITTED_SNAPSHOT을 OFF로 설정하거나 WITH (SNAPSHOT) 같은 테이블 수준 힌트를 사용하여 메모리 최적화 테이블에 대해 지원되는 격리 수준을 제공합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  