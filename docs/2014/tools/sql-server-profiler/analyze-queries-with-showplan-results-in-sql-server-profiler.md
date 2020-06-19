---
title: SQL Server Profiler에서 SHOWPLAN 결과로 쿼리 분석 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], Showplan
- Profiler [SQL Server Profiler], Showplan results
- SQL Server Profiler, Showplan results
ms.assetid: 6a2f7727-141c-4f59-8613-2e452bc78467
author: stevestein
ms.author: sstein
ms.openlocfilehash: 284dfdbd57dde61c92d4cb368371ebe3b1ae6913
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064106"
---
# <a name="analyze-queries-with-showplan-results-in-sql-server-profiler"></a>SQL Server Profiler에서 SHOWPLAN 결과로 쿼리 분석
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 추적에 쿼리 계획 정보를 수집하고 표시하도록 추적 정의에 Showplan 이벤트 클래스를 추가할 수 있습니다. 추적에 수집된 다른 이벤트에서 Showplan 이벤트를 추출하고 이러한 Showplan 이벤트를 별도의 XML 파일에 저장할 수도 있습니다.  
  
 추적에서 Showplan 이벤트를 추출하는 것은 다음 방법 중 하나로 수행할 수 있습니다.  
  
-   추적 구성 시 **이벤트 추출 설정** 탭을 사용합니다. 이 탭은 **이벤트 선택** 탭에서 Showplan 이벤트 중 하나를 선택할 때까지 나타나지 않습니다.  
  
-   **파일** 메뉴에서 **SQL Server 이벤트 추출** 옵션을 사용합니다.  
  
-   특정 이벤트를 마우스 오른쪽 단추로 클릭하고 **이벤트 데이터 추출**을 선택하여 개별 이벤트를 추출 및 저장합니다.  
  
## <a name="showplan-events"></a>Showplan 이벤트  
 Showplan 추적 이벤트는 다음 표에 나열 및 설명되어 있습니다.  
  
|이벤트 이름|Description|  
|----------------|-----------------|  
|**Performance statistics**|처음으로 컴파일된 실행 계획이 캐시된 때와 다시 컴파일된 때, 계획 캐시에서 삭제된 때를 나타냅니다. **TextData** 열에는 XML 형식의 실행 계획이 포함됩니다. 자세한 내용은 [Performance Statistics 이벤트 클래스](../../relational-databases/event-classes/performance-statistics-event-class.md)를 참조하세요.|  
|**Showplan All**|실행된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 전체 컴파일 정보와 쿼리 계획을 표시합니다. 예를 들어 비용 계산 및 열 목록이 표시될 수 있습니다. 자세한 내용은 [Showplan All Event Class](../../relational-databases/event-classes/showplan-all-event-class.md)을 참조하세요.|  
|**Showplan All For Query Compile**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 쿼리가 컴파일 또는 다시 컴파일될 경우 발생합니다. 이는 컴파일 시간에 관련된 **Showplan All** 이벤트입니다. **Showplan All** 은 쿼리가 실행될 때 발생합니다. **Showplan All For Query Compile** 은 쿼리가 컴파일될 때 발생합니다. 자세한 내용은 [Showplan All for Query Compile Event Class](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)을 참조하세요.|  
|**Showplan Statistics Profile**|각 작업을 통해 전달되는 행의 실제 수를 포함하여 실행 중인 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 전체 런타임 정보와 쿼리 계획을 표시합니다. 자세한 내용은 [Showplan Statistics Profile Event Class](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)을 참조하세요.|  
|**Showplan Text**|실행 중인 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 쿼리 계획 트리를 이진 데이터로 표시합니다. 자세한 내용은 [Showplan Text Event Class](../../relational-databases/event-classes/showplan-text-event-class.md)을 참조하세요.|  
|**Showplan Text (Unencoded)**|실행 중인 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 쿼리 계획 트리를 텍스트로 표시합니다. 이 이벤트 클래스는 이진 데이터 대신 텍스트를 표시하는 것을 제외하고 같은 정보를 실행 계획 텍스트로 표시합니다. 자세한 내용은 [Showplan Text&#40;Unencoded&#41; 이벤트 클래스](../../relational-databases/event-classes/showplan-text-unencoded-event-class.md)를 참조하세요.|  
|**Showplan XML**|쿼리 최적화 중 수집된 전체 데이터와 쿼리 계획을 표시합니다. 이 이벤트는 쿼리 계획이 최적화될 때만 생성됩니다. 자세한 내용은 [Showplan XML Event Class](../../relational-databases/event-classes/showplan-xml-event-class.md)을 참조하세요.|  
|**Showplan XML For Query Compile**|쿼리가 컴파일될 때 쿼리 계획을 표시합니다. 자세한 내용은 [Showplan XML for Query Compile Event Class](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)을 참조하세요.|  
|**Showplan XML Statistics Profile**|전체 런타임 정보와 쿼리 계획을 XML 형식으로 표시합니다. 예를 들어 이 이벤트 클래스는 실행되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 각 연산자를 통해 전달되는 행의 수를 캡처합니다. 자세한 내용은 [Showplan XML Statistics Profile Event Class](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [Performance 이벤트 범주](../../relational-databases/event-classes/performance-event-category.md)  
  
  
