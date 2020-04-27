---
title: 추적 템플릿 속성 (이벤트 선택 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetemplateproperties.eventsselection.f1
helpviewer_keywords:
- Trace Template Properties dialog box
ms.assetid: 5b202457-ab42-4902-8012-7f3f40aa09f5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8d86515646236916a9c651c7fa02923b88b995cd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089553"
---
# <a name="trace-template-properties-events-selection-tab"></a>추적 템플릿 속성(이벤트 선택 탭)
  **추적 템플릿 속성** 대화 상자의 **이벤트 선택** 탭을 사용하여 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 추적 템플릿에 포함할 이벤트 클래스와 데이터 열을 표시, 편집 또는 지정할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **Events** 열  
 이벤트 열에서 확인란을 선택하거나 선택 취소하여 추적해야 할 이벤트를 지정합니다. 이벤트는 이벤트 범주별로 구성됩니다.  
  
 **일반** 탭에서 **기존 템플릿을 바탕으로 새 템플릿 만들기** 를 선택한 경우 지정한 템플릿에 따라 이벤트가 자동으로 선택됩니다. 이벤트 클래스에 대한 자세한 내용은 [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조하십시오.  
  
 데이터 열  
 필요한 데이터 열과 이벤트에 해당하는 확인란을 선택하여 추적해야 할 데이터 열을 지정합니다. 이벤트에 해당하는 확인란을 선택한 경우 추적에 포함된 이벤트마다 관련된 모든 이벤트 열이 기본적으로 선택되어 있습니다. **일반** 탭에서 **기존 템플릿을 바탕으로 새 템플릿 만들기** 를 선택한 경우 지정한 템플릿에 따라 데이터 열과 필터가 자동으로 선택됩니다.  
  
 데이터 열 머리글을 클릭하고 필터 조건을 입력하여 필터를 지정합니다. 필터링된 데이터 열은 **필터 편집** 대화 상자에서 열 레이블 왼쪽에 있는 필터 아이콘으로 표시됩니다.  
  
 **모든 이벤트 표시**  
 사용할 수 있는 모든 이벤트를 표시합니다. 기존 템플릿을 기반으로 하지 않고 새 템플릿을 만드는 중이면 이 옵션이 기본적으로 선택되어 있습니다. **이벤트 선택** 표에서 선택되지 않은 이벤트를 모두 숨기려면 확인란의 선택을 취소합니다.  
  
 **모든 열 표시**  
 사용할 수 있는 모든 데이터 열을 표시합니다. 기존 템플릿을 기반으로 하지 않고 새 템플릿을 만드는 중이면 이 옵션이 기본적으로 선택되어 있습니다. **이벤트 선택** 표에서 선택되지 않은 데이터 열을 모두 숨기려면 확인란의 선택을 취소합니다.  
  
 **열 필터**  
 데이터 열 레이블 왼쪽에 필터 아이콘을 표시하는 **필터 편집** 대화 상자를 시작합니다. **필터 편집** 대화 상자를 사용하여 데이터 열 필터를 편집할 수 있습니다.  
  
 **열 구성**  
 추적의 열 순서를 변경하고 결과를 하나 이상의 열로 그룹화합니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 파일 &#40;SQL Server Profiler&#41;에 대 한 이벤트 및 데이터 열을 지정 합니다.](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [추적 &#40;SQL Server Profiler에 표시 되는 열 구성&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [추적 &#40;SQL Server Profiler&#41;에서 이벤트를 필터링 합니다.](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [SQL Server Profiler&#41;&#40;필터 정보 보기](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [필터 &#40;SQL Server Profiler를 수정&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server Profiler 템플릿 및 권한](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
