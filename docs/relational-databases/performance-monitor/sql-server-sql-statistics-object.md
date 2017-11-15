---
title: "SQL Server, SQL Statistics 개체 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:SQL Statistics
- SQL Statistics object
ms.assetid: da7dbb4b-f632-45a0-b1ab-c35cc2695c86
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82c9a520edf0f65e3197d43ad5ef50a8e12b7068
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-sql-statistics-object"></a>SQL Server, SQL Statistics 개체
  **의** SQLServer:SQL Statistics [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 보낸 컴파일과 요청 유형을 모니터링하는 카운터를 제공합니다. 쿼리 컴파일 및 다시 컴파일 수와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 받은 일괄 처리 수를 모니터링하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 사용자 쿼리를 처리하는 속도와 쿼리 최적화 프로그램이 쿼리를 처리하는 효율을 알 수 있습니다.  
  
 컴파일은 쿼리 반환 시간의 중요한 부분을 차지합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 컴파일 비용을 줄이기 위해 컴파일된 쿼리 계획을 쿼리 캐시에 보관합니다. 캐시의 목적은 컴파일된 쿼리를 다시 사용할 수 있도록 보관하여 컴파일 작업을 줄이고 다음 쿼리를 실행할 때 다시 컴파일할 필요를 없애는 것입니다. 그러나 각각의 고유한 쿼리는 적어도 한 번은 컴파일해야 합니다. 다음 요인이 발생하면 쿼리를 다시 컴파일해야 합니다.  
  
-   테이블에 행 또는 인덱스를 추가하는 등의 기본 스키마 변경 또는 테이블에 많은 수의 행을 삽입하거나 삭제하는 등의 통계 스키마 변경을 통한 스키마 변경  
  
-   환경(SET 문) 변경 ANSI_PADDING 또는 ANSI_NULLS 같은 세션 설정을 바꾸면 쿼리를 다시 컴파일해야 합니다.  
  
 단순 매개 변수화 및 강제 매개 변수화 방법은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
 다음은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Statistics** 카운터에 대한 설명입니다.  
  
|SQL Server SQL Statistics 카운터|설명|  
|----------------------------------------|-----------------|  
|**Auto-Param Attempts/sec**|초당 자동 매개 변수화 시도 수입니다. 합계는 자동 매개 변수화의 실패한 횟수, 안전한 횟수 그리고 안전하지 않은 횟수의 합과 같습니다. 자동 매개 변수화는 유사한 여러 요청을 처리할 때 캐시된 결과 실행 계획을 다시 사용하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 일부 리터럴을 매개 변수로 바꾸어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 요청을 매개 변수화할 때 일어납니다. 새로운 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 자동 매개 변수화를 단순 매개 변수화라고도 합니다. 이 카운터에는 강제 매개 변수화는 포함되지 않습니다.|  
|**Batch Requests/sec**|초당 받는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령 일괄 처리 수입니다. 이 통계는 모든 제약 조건(I/O, 사용자 수, 캐시 크기, 요청의 복잡도 등)의 영향을 받습니다. 높은 일괄 처리 수치는 높은 처리 효율을 의미합니다.|  
|**Failed Auto-Params/sec**|실패한 자동 매개 변수화의 초당 시도 횟수입니다. 이 값은 작을수록 좋습니다. 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 자동 매개 변수화를 단순 매개 변수화라고도 합니다.|  
|**Forced Parameterizations/sec**|초당 성공한 강제 매개 변수화 수입니다.|  
|**Guided Plan Executions/sec**|계획 지침을 통해 쿼리 계획이 생성되는 초당 계획 실행 수입니다.|  
|**Misguided Plan Executions/sec**|계획 생성 중에 계획 지침을 적용할 수 없는 초당 계획 실행 수입니다. 계획 지침이 무시되고 일반적인 컴파일을 사용하여 실행된 계획이 생성됩니다.|  
|**Safe Auto-Params/sec**|안전한 자동 매개 변수화의 초당 시도 횟수입니다. 안전한 자동 매개 변수화는 여러 유사한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 간에 캐시된 실행 계획을 공유할 수 있도록 하는 결정을 참조하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시도하는 많은 자동 매개 변수화 중 일부는 성공하고 나머지는 실패합니다. 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 자동 매개 변수화를 단순 매개 변수화라고도 합니다. 강제 매개 변수화는 포함되지 않습니다.|  
|**SQL Attention rate**|초당 주의 수입니다. 주의는 현재 실행 중인 요청을 종료하기 위한 클라이언트의 요청입니다.|  
|**SQL Compilations/sec**|초당 SQL 컴파일 수입니다. 컴파일 코드 경로를 입력한 횟수를 나타내며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 문 수준의 다시 컴파일에 의한 컴파일을 포함합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 작업이 안정되면 이 값은 일정한 수준에 이릅니다.|  
|**SQL Re-Compilations/sec**|초당 문 다시 컴파일 수입니다. 문 다시 컴파일이 트리거된 횟수를 나타냅니다. 일반적으로 다시 컴파일하는 횟수는 적을수록 좋습니다.|  
|**Unsafe Auto-Params/sec**|안전하지 않은 자동 매개 변수화의 초당 시도 횟수입니다. 예를 들어 쿼리는 캐시된 계획을 공유하지 않고 자동 매개 변수화하는 특성이 있습니다. 이러한 자동 매개 변수화는 안전하지 않은 것으로 지정됩니다. 강제 매개 변수화 수는 여기에 포함되지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server, Plan Cache 개체](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
