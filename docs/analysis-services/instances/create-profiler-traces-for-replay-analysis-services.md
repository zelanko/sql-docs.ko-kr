---
title: 재생 (Analysis Services)에 대 한 프로파일러 추적 만들기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d5928325ffe5b0b98da2058529b1cbb036a445be
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34014790"
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>재생에 대한 프로파일러 추적 만들기(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  사용자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 필요한 이벤트를 수집해야 합니다. 이러한 이벤트의 컬렉션을 초기화하려면 **추적 속성** 대화 상자의 **이벤트 선택** 탭에서 적합한 이벤트 클래스를 선택해야 합니다. 예를 들어 Query Begin 이벤트 클래스가 선택된 경우 쿼리를 포함한 이벤트가 수집되고 재생에 사용됩니다. 또한 추적 파일에는 원래 트랜잭션 시퀀스로 분산 환경에서 서버 트랜잭션 재생을 지원하는 데 충분한 정보가 포함됩니다.  
  
## <a name="replay-for-queries"></a>쿼리 재생  
 쿼리를 재생하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 다음 이벤트를 캡처해야 합니다.  
  
-   모든 데이터 열을 갖는 Audit Login 이벤트 클래스. 이 이벤트 클래스는 로그인한 사용자 및 세션 설정에 대한 정보를 제공합니다. SPID(서버 프로세스 ID)는 사용자 세션에 대한 참조를 제공합니다. 자세한 내용은 [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Query Begin 이벤트 클래스. 이 이벤트 클래스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 전송된 쿼리에 대한 정보를 제공합니다. Event Subclass 열은 쿼리 유형에 대한 정보를 제공합니다. TextData 열은 쿼리의 실제 텍스트를 제공합니다. RequestParameters 열은 매개 변수가 있는 쿼리의 매개 변수를 제공하고 RequestProperties 열은 XMLA(XML for Analysis) 요청의 속성을 제공합니다. 자세한 내용은 [Queries Events Data Columns](../../analysis-services/trace-events/queries-events-data-columns.md)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Query End 이벤트 클래스. 이 이벤트 클래스는 쿼리 실행 상태를 확인합니다. 자세한 내용은 [Queries Events Data Columns](../../analysis-services/trace-events/queries-events-data-columns.md)을 참조하세요.  
  
## <a name="replay-for-discovers"></a>검색 항목 재생  
 검색 항목을 재생하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 다음 이벤트를 캡처해야 합니다.  
  
-   모든 데이터 열을 갖는 Audit Login 이벤트 클래스. 이 이벤트 클래스는 로그인한 사용자 및 세션 설정에 대한 정보를 제공합니다. SPID는 사용자 세션에 대한 참조를 제공합니다. 자세한 내용은 [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Discover Begin 이벤트 클래스. TextData 열은 제공 된 \<RequestType > discover 요청 및 RequestProperties 열의 부분을 제공는 \<속성 > 부분 검색 요청을 합니다. EventSubclass 열은 검색 유형을 제공합니다. 자세한 내용은 [Discover Events Data Columns](../../analysis-services/trace-events/discover-events-data-columns.md)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Discover End 이벤트 클래스. 이 이벤트 클래스는 검색 요청 상태를 확인합니다. 자세한 내용은 [Discover Events Data Columns](../../analysis-services/trace-events/discover-events-data-columns.md)을 참조하세요.  
  
## <a name="replay-for-commands"></a>명령 재생  
 명령을 재생하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 다음 이벤트를 캡처해야 합니다.  
  
-   모든 데이터 열을 갖는 Command Begin 이벤트 클래스. TextData 열은 프로세스 유형, 데이터베이스 ID 및 큐브 ID와 같은 명령 세부 정보를 제공합니다. RequestParameters 열은 매개 변수가 있는 명령의 매개 변수를 제공하고 RequestProperties 열은 XMLA 요청의 속성을 제공합니다. 자세한 내용은 [Command Events Data Columns](../../analysis-services/trace-events/command-events-data-columns.md)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Command End 이벤트 클래스. 이 이벤트 클래스는 명령 상태를 확인합니다. 자세한 내용은 [Command Events Data Columns](../../analysis-services/trace-events/command-events-data-columns.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [SQL Server Profiler로 Analysis Services 모니터링 소개](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
