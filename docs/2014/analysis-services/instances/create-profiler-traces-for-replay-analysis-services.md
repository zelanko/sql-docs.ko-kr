---
title: 재생 (Analysis Services)에 대 한 Profiler 추적 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- replaying queries
- replaying discovers
- events [Analysis Services]
- replaying commands
- Profiler [SQL Server Profiler], Analysis Services
- performance [Analysis Services], replays
- traces [Analysis Services]
ms.assetid: 93b2fc46-7cfb-4ab5-abeb-1475a7d6f0f2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc494fa63064d5c48c94e44cb91db5b1fe0f988d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080140"
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>재생에 대한 프로파일러 추적 만들기(Analysis Services)
  사용자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 필요한 이벤트를 수집해야 합니다. 이러한 이벤트의 컬렉션을 초기화하려면 **추적 속성** 대화 상자의 **이벤트 선택** 탭에서 적합한 이벤트 클래스를 선택해야 합니다. 예를 들어 Query Begin 이벤트 클래스가 선택된 경우 쿼리를 포함한 이벤트가 수집되고 재생에 사용됩니다. 또한 추적 파일에는 원래 트랜잭션 시퀀스로 분산 환경에서 서버 트랜잭션 재생을 지원하는 데 충분한 정보가 포함됩니다.  
  
## <a name="replay-for-queries"></a>쿼리 재생  
 쿼리를 재생하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 다음 이벤트를 캡처해야 합니다.  
  
-   모든 데이터 열을 갖는 Audit Login 이벤트 클래스. 이 이벤트 클래스는 로그인한 사용자 및 세션 설정에 대한 정보를 제공합니다. SPID(서버 프로세스 ID)는 사용자 세션에 대한 참조를 제공합니다. 자세한 내용은 [Security Audit Data Columns](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Query Begin 이벤트 클래스. 이 이벤트 클래스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 전송된 쿼리에 대한 정보를 제공합니다. Event Subclass 열은 쿼리 유형에 대한 정보를 제공합니다. TextData 열은 쿼리의 실제 텍스트를 제공합니다. RequestParameters 열은 매개 변수가 있는 쿼리의 매개 변수를 제공하고 RequestProperties 열은 XMLA(XML for Analysis) 요청의 속성을 제공합니다. 자세한 내용은 [Queries Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Query End 이벤트 클래스. 이 이벤트 클래스는 쿼리 실행 상태를 확인합니다. 자세한 내용은 [Queries Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns)을 참조하세요.  
  
## <a name="replay-for-discovers"></a>검색 항목 재생  
 검색 항목을 재생하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 다음 이벤트를 캡처해야 합니다.  
  
-   모든 데이터 열을 갖는 Audit Login 이벤트 클래스. 이 이벤트 클래스는 로그인한 사용자 및 세션 설정에 대한 정보를 제공합니다. SPID는 사용자 세션에 대한 참조를 제공합니다. 자세한 내용은 [Security Audit Data Columns](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Discover Begin 이벤트 클래스. TextData 열은 제공 합니다 \<RequestType > 검색 요청을 하 고 RequestProperties 열에 대 한 부분을 제공는 \<속성 > discover 요청 부분입니다. EventSubclass 열은 검색 유형을 제공합니다. 자세한 내용은 [Discover Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Discover End 이벤트 클래스. 이 이벤트 클래스는 검색 요청 상태를 확인합니다. 자세한 내용은 [Discover Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns)을 참조하세요.  
  
## <a name="replay-for-commands"></a>명령 재생  
 명령을 재생하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 다음 이벤트를 캡처해야 합니다.  
  
-   모든 데이터 열을 갖는 Command Begin 이벤트 클래스. TextData 열은 프로세스 유형, 데이터베이스 ID 및 큐브 ID와 같은 명령 세부 정보를 제공합니다. RequestParameters 열은 매개 변수가 있는 명령의 매개 변수를 제공하고 RequestProperties 열은 XMLA 요청의 속성을 제공합니다. 자세한 내용은 [Command Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns)을 참조하세요.  
  
-   모든 데이터 열을 갖는 Command End 이벤트 클래스. 이 이벤트 클래스는 명령 상태를 확인합니다. 자세한 내용은 [Command Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 추적 이벤트](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [SQL Server 프로파일러를 사용한 Analysis Services 모니터링 소개](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
