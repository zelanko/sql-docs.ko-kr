---
title: 추적 파일 속성 (이벤트 선택 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracefileproperties.eventsselection.f1
helpviewer_keywords:
- Trace File Properties dialog box
ms.assetid: 158d442f-2225-4173-8545-fb1cf611b4d0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a6c6da76bd89b4686791087e558ae1f329f57a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088798"
---
# <a name="trace-file-properties-events-selection-tab"></a>추적 파일 속성(이벤트 선택 탭)
  
  **추적 파일 템플릿 속성** 대화 상자의 **이벤트 선택** 탭을 사용하여 추적의 열 속성을 보거나 추적에서 데이터 열을 제거할 수 있습니다.  
  
 이 창을 보려면 추적 파일을 엽니다. 그런 다음 **파일** 메뉴에서 **속성**을 클릭 하 고 **이벤트 선택** 탭을 클릭 합니다.  
  
## <a name="options"></a>옵션  
 **Events** 열  
 이벤트 범주별로 구성된 추적된 이벤트를 표시합니다. 처음에는 추적의 모든 이벤트가 선택됩니다. 이벤트는 해당 확인란을 선택하거나 이벤트에 대한 데이터 열을 선택하여 선택할 수 있습니다. 이벤트 확인란을 선택하면 해당 이벤트에 대해 사용할 수 있는 모든 데이터 열이 선택됩니다. 이벤트에 대한 데이터 열을 선택하면 이벤트가 선택되고 필요한 다른 열도 자동으로 선택됩니다. 추적 파일 또는 테이블을 볼 때 이벤트 또는 데이터 열에 대한 확인란의 선택을 취소하면 추적 창에 표시되는 데이터의 양이 줄어들므로 보다 쉽게 분석할 수 있습니다. 추적 창에 표시되는 데이터의 양은 열 필터를 변경하여 줄일 수도 있습니다. 이벤트 클래스에 대한 자세한 내용은 [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조하십시오.  
  
 데이터 열  
 추적된 데이터 열을 표시합니다. 추적에 포함된 각 이벤트에 대해 기본적으로 추적의 모든 관련 데이터 열이 선택됩니다.  
  
 데이터 열 머리글을 클릭하고 필터 조건을 입력하여 필터를 지정합니다. 필터링된 데이터 열은 **필터 편집** 대화 상자에서 열 레이블 왼쪽에 있는 필터 아이콘으로 표시됩니다.  
  
 **모든 이벤트 표시**  
 사용할 수 있는 모든 이벤트를 표시합니다. 기본적으로 **이벤트 선택** 표에서 선택된 행만 표시됩니다. 
  **이벤트 선택** 표에서 선택되지 않은 모든 이벤트를 숨기려면 이 확인란의 선택을 취소합니다. 
  **모든 이벤트 표시** 를 선택한 상태에서 추적 파일 또는 테이블을 볼 때는 추적에 기록된 모든 이벤트가 추적 창에 표시됩니다.  
  
 **모든 열 표시**  
 사용할 수 있는 모든 데이터 열을 표시합니다. 기본적으로 선택된 데이터 열만 표시됩니다. 
  **이벤트 선택** 표에서 선택되지 않은 모든 데이터 열을 숨기려면 이 확인란의 선택을 취소합니다.  
  
 **열 필터**  
 
  **필터 편집** 대화 상자를 시작합니다. 필터링된 데이터 열의 열 레이블 왼쪽에 필터 아이콘이 표시됩니다. 
  **필터 편집** 대화 상자를 사용하여 데이터 열 필터를 편집할 수 있습니다.  
  
 **열 구성**  
 
  **이벤트** 를 선택하고 추적할 데이터 열을 선택한 다음 **열 구성** 을 클릭하여 추적 결과 창에서 표에 있는 열의 순서를 다시 정렬합니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 파일 &#40;SQL Server Profiler&#41;에 대 한 이벤트 및 데이터 열을 지정 합니다.](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [추적 &#40;SQL Server Profiler&#41;에서 이벤트를 필터링 합니다.](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [SQL Server Profiler&#41;&#40;필터 정보 보기](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [필터 &#40;SQL Server Profiler를 수정&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server 프로파일러](../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler 템플릿 및 권한](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
  
  
