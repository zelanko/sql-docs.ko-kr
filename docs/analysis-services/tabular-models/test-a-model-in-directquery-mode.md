---
title: DirectQuery 모드에서 모델을 테스트 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eae53b4edbcc542154d627a748321810c2059d59
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039723"
---
# <a name="test-a-model-in-directquery-mode"></a>DirectQuery 모드에서 모델 테스트
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  디자인부터 시작하여 각 개발 단계에서 DirectQuery 모드로 테이블 형식 모델을 테스트하기 위한 옵션을 검토합니다.  
  
## <a name="test-in-excel"></a>Excel에서 테스트 
  
 SSDT에서 모델을 디자인하는 경우 **Excel에서 분석** 기능을 사용하여 메모리의 샘플 데이터 집합이나 관계형 데이터베이스에 대해 모델링 결정을 테스트할 수 있습니다.  Excel에서 분석을 클릭하면 옵션을 지정할 수 있는 대화 상자가 열립니다.
 
 ![Excel DirectQuery 옵션에서 분석](../../analysis-services/tabular-models/media/analyze-in-excel-directquery-options.png)
 
 모델의 DirectQuery 모드가 켜져 있으면 두 가지 옵션이 있는 DirectQuery 연결 모드를 지정할 수 있습니다.
 - **샘플 데이터 뷰** - 이 옵션을 사용하면 Excel의 모든 쿼리가 메모리에 샘플 데이터 집합을 포함하는 샘플 파티션으로 전달됩니다. 이 옵션은 측정값, 계산 열 또는 행 수준 보안에 있는 DAX 수식이 올바르게 수행되게 하려는 경우에 유용합니다.
 
 - **전체 데이터 뷰** - 이 옵션을 사용하면 Excel의 모든 쿼리가 Analysis Services, 관계형 데이터베이스로 차례로 전달됩니다. 이 옵션은 실제로 완벽하게 작동하는 DirecQuery 모드입니다.
 
 ### <a name="other-clients"></a>다른 클라이언트
 Excel에서 분석을 사용하는 경우 .odc 연결 파일이 생성됩니다. 이 파일의 연결 문자열 정보를 사용하여 다른 클라이언트 응용 프로그램에서 모델에 연결할 수 있습니다. 클라이언트가 샘플 데이터 파티션에 연결하도록 지정하기 위해 DataView=Sample 매개 변수가 추가됩니다.  
  
## <a name="monitor-query-execution-on-backend-systems-using-xevents-or-sql-profiler"></a>xEvents 또는 SQL 프로파일러를 사용하여 백 엔드 시스템에서 쿼리 실행을 모니터링 
 SQL Server 관계형 데이터베이스에 연결된 세션 추적을 시작하여 테이블 형식 모델에서 수신되는 연결을 모니터링합니다.  
  
-   [SQL Server 확장 이벤트를 사용하여 Analysis Services 모니터링](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
-   [SQL Server Profiler를 사용 하 여 Analysis Services 모니터링](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
 Oracle 또는 Teradata를 사용하는 경우 해당 시스템용 추적 모니터링 도구를 사용하세요.  
  
  
