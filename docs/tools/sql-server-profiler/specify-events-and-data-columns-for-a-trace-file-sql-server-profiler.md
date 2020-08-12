---
title: 추적 파일에 대해 이벤트 및 데이터 열 지정
titleSuffix: SQL Server Profiler
description: SQL Server Profiler가 추적에서 이벤트 데이터를 캡처할 때 포함할 이벤트 클래스와 데이터 열을 지정하는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 7da715a3-2f03-4063-b6a4-20fd7b44e675
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 624ee18dfeb1fb73f0b7ba77eab8466ab90f6130
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734187"
---
# <a name="specify-events-and-data-columns-for-a-trace-file-sql-server-profiler"></a>추적 파일에 대해 이벤트 및 데이터 열 지정(SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적에 대해 이벤트 클래스 및 데이터 열을 지정하는 방법에 대해 설명합니다.  
  
### <a name="to-specify-events-and-data-columns-for-a-trace"></a>추적에 대해 이벤트 및 데이터 열을 지정하려면  
  
1.  **추적 속성** 또는 **추적 템플릿 속성** 대화 상자에서 **이벤트 선택** 탭을 클릭합니다.  
  
     **이벤트 선택** 탭에는 표 형태 컨트롤이 있습니다. 표 형태 컨트롤은 추적 가능한 각 이벤트 클래스가 들어 있는 테이블입니다. 테이블에는 각 이벤트 클래스에 대한 행이 하나씩 포함되어 있습니다. 이벤트 클래스는 연결한 서버의 유형 및 버전에 따라 약간 다를 수 있습니다. 이벤트 클래스는 표의 **이벤트**열에서 식별되며 이벤트 범주별로 그룹화됩니다. 나머지 열은 각 이벤트 클래스에 대해 반환할 수 있는 데이터 열을 나열합니다.  
  
2.  **이벤트 선택**탭에서 표 형태 컨트롤을 사용하여 이벤트와 데이터 열을 추적 파일에서 추가하거나 제거합니다.  
  
3.  추적에서 이벤트를 제거하려면 각 이벤트 클래스에 대한 **이벤트** 열의 확인란을 선택 취소합니다.  
  
4.  추적에 이벤트를 포함하려면 각 이벤트 클래스에 대한 **이벤트** 열에서 확인란을 선택하거나 이벤트에 해당하는 데이터 열을 선택합니다.  
  
> [!IMPORTANT]  
>  추적에 시스템 모니터 또는 성능 모니터 데이터와의 상관 관계를 지정하려면 **Start Time** 및 **End Time** 데이터 열이 모두 추적에 포함되어야 합니다.  
  
 이벤트 클래스를 포함할 때 이벤트에 해당되는 확인란을 선택한 경우 연관된 데이터 열도 모두 추적에 포함됩니다. 특정 열에 대해 확인란을 선택한 경우에는 해당 열만 추적에 포함됩니다.  
  
1.  이벤트 클래스에서 데이터 열을 제거하려면 이벤트 클래스 행의 데이터 열에서 확인란 선택을 취소하거나 열 머리글을 마우스 오른쪽 단추로 클릭하고 **열 선택 취소** 옵션을 선택합니다.  
  
2.  필요에 따라 추적에 필터를 적용합니다. 자세한 내용은 [추적에서의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
