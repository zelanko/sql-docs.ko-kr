---
title: Errors and Warnings 이벤트 범주(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 4ca754e745a523262b18754284ebb7bc33122d88
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565717"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Errors and Warnings 이벤트 범주(데이터베이스 엔진)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Errors and Warnings** 이벤트 범주에는 일반적인 오류 및 경고 이벤트가 포함되어 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[Attention 이벤트 클래스](../../relational-databases/event-classes/attention-event-class.md)|**Attention** 이벤트가 발생했음을 나타냅니다.|  
|[Background Job Error 이벤트 클래스](../../relational-databases/event-classes/background-job-error-event-class.md)|백그라운드 작업이 비정상적으로 종료되었음을 나타냅니다.|  
|[Bitmap Warning 이벤트 클래스](../../relational-databases/event-classes/bitmap-warning-event-class.md)|쿼리에서 비트맵 필터링을 사용하지 않도록 설정했음을 나타냅니다.|  
|[Blocked Process Report 이벤트 클래스](../../relational-databases/event-classes/blocked-process-report-event-class.md)|지정된 기간보다 그 이상으로 태스크가 차단되었음을 나타냅니다.|  
|[CPU Threshold Exceeded 이벤트 클래스](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)|리소스 관리자가 지정된 CPU 임계값을 초과하는 쿼리를 감지했음을 나타냅니다.|  
|[ErrorLog 이벤트 클래스](../../relational-databases/event-classes/errorlog-event-class.md)|오류 이벤트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 기록되었음을 나타냅니다.|  
|[EventLog 이벤트 클래스](../../relational-databases/event-classes/eventlog-event-class.md)|이벤트가 Windows 이벤트 로그에 기록되었음을 나타냅니다.|  
|[Exception 이벤트 클래스](../../relational-databases/event-classes/exception-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 예외가 발생했음을 나타냅니다.|  
|[Exchange Spill 이벤트 클래스](../../relational-databases/event-classes/exchange-spill-event-class.md)|병렬 쿼리 계획의 통신 버퍼가 tempdb 데이터베이스에 기록되었음을 나타냅니다.|  
|[Execution Warnings 이벤트 클래스](../../relational-databases/event-classes/execution-warnings-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문이나 저장 프로시저 실행 중에 메모리 부여 경고가 발생했음을 나타냅니다.|  
|[Hash Warning 이벤트 클래스](../../relational-databases/event-classes/hash-warning-event-class.md)|해시 연산 중 해시 재귀 또는 해시 재귀 한도 초과가 발생했음을 나타냅니다.|  
|[Missing Column Statistics 이벤트 클래스](../../relational-databases/event-classes/missing-column-statistics-event-class.md)|최적화 프로그램에 유용한 열 통계를 사용할 수 없음을 나타냅니다.|  
|[Missing Join Predicate 이벤트 클래스](../../relational-databases/event-classes/missing-join-predicate-event-class.md)|조인 조건자가 없는 쿼리가 실행되고 있음을 나타냅니다.|  
|[Sort Warnings 이벤트 클래스](../../relational-databases/event-classes/sort-warnings-event-class.md)|정렬 작업이 메모리에 적합하지 않음을 나타냅니다.|  
|[User Error Message 이벤트 클래스](../../relational-databases/event-classes/user-error-message-event-class.md)|사용자에게 표시되는 오류 메시지를 보여 줍니다.|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
