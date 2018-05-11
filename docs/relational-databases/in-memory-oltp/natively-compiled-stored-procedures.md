---
title: 고유하게 컴파일된 저장 프로시저 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c5d3c56f0a8c725136b3b21fd41138fceb34f87d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="natively-compiled-stored-procedures"></a>Natively Compiled Stored Procedures
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  고유하게 컴파일된 저장 프로시저는 메모리 최적화 테이블에 액세스하는 네이티브 코드로 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저입니다. 고유하게 컴파일된 저장 프로시저는 쿼리 및 비즈니스 논리가 저장 프로시저에서 효율적으로 실행되도록 해 줍니다. 네이티브 컴파일 프로세스에 대한 자세한 내용은 [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md)을 참조하세요. 디스크 기반 저장 프로시저를 고유하게 컴파일된 저장 프로시저로 마이그레이션하는 방법은 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)를 참조하세요.  
  
> [!NOTE]  
>  해석된(디스크 기반) 저장 프로시저와 고유하게 컴파일된 저장 프로시저 간의 한 가지 차이점은 해석된 저장 프로시저가 처음 실행할 때 컴파일되는 반면 고유하게 컴파일된 저장 프로시저는 생성할 때 컴파일된다는 것입니다. 고유하게 컴파일된 저장 프로시저를 사용하면 만들 때 많은 오류 조건을 검색하여 고유하게 컴파일된 저장 프로시저 만들기가 실패할 수 있습니다(예: 산술 오버플로, 형식 변환, 일부 0으로 나누기 조건). 해석된 저장된 프로시저를 사용하면 일반적으로 저장 프로시저를 만들 때 이러한 오류 조건으로 인해 오류가 발생하지 않지만 모든 실행이 실패합니다.  
  
 이 섹션의 항목:  
  
-   [고유하게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)  
  
-   [ATOMIC 블록](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)  
  
-   [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 DDL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [고유하게 컴파일된 저장 프로시저 및 Execution Set 옵션](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [고유하게 컴파일된 저장 프로시저를 호출하는 최선의 구현 방법](../../relational-databases/in-memory-oltp/best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [고유하게 컴파일된 저장 프로시저의 성능 모니터링](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [데이터 액세스 응용 프로그램에서 고유하게 컴파일된 저장 프로시저 호출](../../relational-databases/in-memory-oltp/calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
