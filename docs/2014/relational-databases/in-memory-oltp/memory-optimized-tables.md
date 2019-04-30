---
title: 메모리 액세스에 최적화 된 테이블 | Microsoft 문서
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14dddf81-b502-49dc-a6b6-d18b1ae32d2b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9123bf89f75fce68a6edd8ba1becd141821fe326
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63158757"
---
# <a name="memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 내 OLTP는 효율적이고 메모리 최적화 데이터 액세스, 비즈니스 논리의 고유 컴파일, 잠금 및 래치 없는 알고리즘을 통해 OLTP 애플리케이션의 성능을 향상하는 데 도움이 됩니다. 메모리 내 OLTP 기능에는 메모리 최적화 테이블 및 테이블 형식뿐 아니라 이 테이블에 효율적으로 액세스하기 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 고유 컴파일도 포함됩니다.  
  
 메모리 최적화 테이블에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [메모리 액세스에 최적화된 테이블 소개](memory-optimized-tables.md)  
  
     메모리 최적화 테이블에 대해 자세히 설명하고 데이터 내구성, 메모리 최적화 테이블의 데이터에 대한 액세스, 성능 및 확장성에 대한 정보를 제공합니다.  
  
-   [테이블과 저장 프로시저의 네이티브 컴파일](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
     메모리 최적화 테이블과 고유하게 컴파일된 저장 프로시저가 DLL에 컴파일되는 방법을 자세히 설명하며 관련 보안 고려 사항을 제공합니다.  
  
-   [메모리 액세스에 최적화된 테이블 변경](altering-memory-optimized-tables.md)  
  
     메모리 최적화 테이블 업데이트에 대한 지침입니다(테이블 열, 인덱스 및 bucket_count 변경 포함).  
  
-   [메모리 액세스에 최적화된 테이블의 트랜잭션 이해](../../database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
     이 섹션에서는 트랜잭션 격리 수준, 크로스 컨테이너 트랜잭션을 비롯하여 메모리 최적화 테이블에서 트랜잭션 수행과 관련된 여러 가지 항목을 제공합니다.  
  
-   [메모리 액세스에 최적화된 테이블 분할을 위한 응용 프로그램 패턴](application-pattern-for-partitioning-memory-optimized-tables.md)  
  
     메모리 최적화 테이블을 사용할 때 분할된 테이블을 에뮬레이트하는 방법을 보여 주는 자세한 코드 샘플입니다.  
  
-   [메모리 액세스에 최적화된 테이블에 대한 통계](statistics-for-memory-optimized-tables.md)  
  
     메모리 최적화 테이블에 대해 통계를 컴파일하는 방법과 메모리 최적화 테이블을 유지 관리하고 수동으로 업데이트하는 방법에 대해 자세히 설명합니다.  
  
-   [데이터 정렬 및 코드 페이지](../../database-engine/collations-and-code-pages.md)  
  
     메모리 최적화 테이블에 대해 지원되는 데이터 정렬 및 코드 페이지 제한에 대해 자세히 설명합니다.  
  
-   [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](table-and-row-size-in-memory-optimized-tables.md)  
  
     메모리 최적화 테이블 행의 8060바이트 제한에 대해 자세히 설명하고 테이블 및 행 크기 계산 예제를 제공합니다.  
  
-   [메모리 액세스에 최적화된 테이블에 대한 쿼리 처리 가이드](a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
     메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저 모두의 쿼리 처리에 대한 개요를 제공합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
