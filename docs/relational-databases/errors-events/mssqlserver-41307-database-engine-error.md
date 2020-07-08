---
title: MSSQLSERVER_41307 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e3442e56275c3ebae663cab1e027ab82298081c8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85694607"
---
# <a name="mssqlserver_41307"></a>MSSQLSERVER_41307
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41307|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HK_HEKATON_ROW_LIMIT|  
|메시지 텍스트|메모리 액세스에 최적화된 테이블의 행 크기 제한인 *number*바이트를 초과했습니다. 테이블 정의를 단순하게 만드십시오.|  
  
## <a name="explanation"></a>설명  
메모리 액세스에 최적화된 테이블의 행 크기 제한은 8,060바이트입니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](~/relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)를 참조하세요. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
