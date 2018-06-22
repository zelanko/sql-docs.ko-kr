---
title: MSSQLSERVER_41307 | Microsoft 문서
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
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7be8ecc62c65020daa7f376960a8184367662189
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089574"
---
# <a name="mssqlserver41307"></a>MSSQLSERVER_41307
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41307|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HK_HEKATON_ROW_LIMIT|  
|메시지 텍스트|메모리 액세스에 최적화된 테이블의 행 크기 제한인 *number*바이트를 초과했습니다. 테이블 정의를 단순하게 만드십시오.|  
  
## <a name="explanation"></a>설명  
 메모리 액세스에 최적화된 테이블의 행 크기 제한은 8,060바이트입니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](../in-memory-oltp/memory-optimized-tables.md)를 참조하세요. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  