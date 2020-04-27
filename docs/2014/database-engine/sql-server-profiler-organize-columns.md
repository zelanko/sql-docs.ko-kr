---
title: 열 SQL Server Profiler 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.organize.columns.f1
ms.assetid: bf5674f4-da5e-43f9-aeb2-76ca37993790
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0ad3d1204e8c27d91ecb3b586d56a27d45eeb4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089761"
---
# <a name="sql-server-profiler---organize-columns"></a>SQL Server 프로파일러 - 열 구성
  **열 구성** 대화 상자를 사용하여 데이터 열을 선택한 후 추적 파일에 표시되는 이벤트를 그룹화하거나 집계하면 큰 추적 파일 또는 테이블을 쉽게 확인 및 분석할 수 있습니다.  
  
 집계할 경우 해당 이벤트 클래스 형식의 추적에 포함된 모든 이벤트가 이동 또는 축소됩니다. 이벤트 클래스 이름의 왼쪽**+** 에 더하기 기호 ()가 나타납니다. 더하기 기호를 클릭하면 이벤트 클래스가 확장되어 해당 형식의 모든 이벤트가 표시됩니다.  
  
 그룹화하면 추적 창 화면에 이벤트 클래스가 형식별로 분류되어 표시됩니다. 그러나 각 이벤트 클래스 형식의 이벤트는 축소되어 표시되지 않습니다.  
  
 추적 창 화면에서 이벤트를 그룹화하거나 집계하면, 그룹화 또는 집계하도록 선택한 열은 창에서 고정되어 있지만 오른쪽 또는 왼쪽으로 스크롤하여 다른 데이터 열을 볼 수 있습니다.  
  
 이 대화 상자에 액세스하려면 기존 추적 파일 또는 테이블을 열고 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] **파일** 메뉴에서 **파일**을 클릭합니다. **추적 속성** 대화 상자에서 **이벤트 선택** 탭을 클릭한 다음 **열 구성**을 클릭합니다. 또한 새 추적을 만들 때 **이벤트 선택** 탭에서 **열 구성** 을 클릭해도 됩니다.  
  
## <a name="options"></a>옵션  
 **그룹**  
 추적 창에서 이벤트 클래스를 그룹화하거나 집계하려면 **그룹** 아래에 있는 데이터 열 이름을 이동합니다.  
  
 이벤트를 집계하려면 데이터 열을 하나씩 **그룹**으로 이동합니다. 그러면 추적 창 화면의 이벤트 형식 이름 아래에 있는 특정 형식의 모든 이벤트가 축소됩니다. 이벤트 클래스 이름의 왼쪽**+** 에 더하기 기호 ()가 나타납니다. 이벤트 클래스 형식을 확장하고 모든 이벤트를 표시하려면 더하기 기호를 클릭합니다. **보기** 메뉴에서 **집계 보기** 또는 **그룹화 보기** 를 클릭하여 집계 및 그룹화 옵션을 설정하거나 해제할 수 있습니다.  
  
 이벤트를 그룹화하려면 둘 이상의 데이터 열을 **그룹**으로 이동합니다. 그러면 추적 창 화면에서 특정 형식의 모든 이벤트가 그룹화되지만 각 이벤트 클래스 형식 이름 아래에 있는 이벤트는 축소되지 않습니다. 보기 메뉴에서 **그룹화 보기** 를 클릭하여 그룹화된 보기와 그룹화되지 않은 보기 간에 전환할 수 있습니다. 데이터 열을 두 개 이상 **그룹**으로 이동한 경우에는 **집계 보기** 로 전환할 수 없습니다.  
  
 **열**  
 **그룹**으로 이동할 수 있는 데이터 열의 목록입니다. 열 왼쪽에 있는 더하기**+** 기호 ()를 클릭 **Columns** 하 여 목록을 확장 합니다.  
  
 **위로**  
 데이터 열을 선택한 다음 **위로** 를 클릭하여 데이터 열을 **그룹**으로 이동합니다. **위로** 를 클릭하여 추적 창 화면에서 열이 표시되는 순서를 다시 정렬할 수도 있습니다.  
  
 **아래로**  
 데이터 열을 선택한 다음 **아래로** 를 클릭하여 데이터 열을 **그룹**밖으로 이동합니다. **아래로** 를 클릭하여 추적 창 화면에서 열이 표시되는 순서를 다시 정렬할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 &#40;SQL Server Profiler에 표시 되는 열 구성&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [추적 &#40;SQL Server Profiler를 만듭니다&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [SQL Server Profiler &#40;추적 템플릿을 만듭니다&#41;](../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [SQL Server Profiler &#40;추적 파일을 엽니다&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
  
