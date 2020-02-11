---
title: SQL Server Profiler로 Analysis Services 모니터링 소개 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 568ec549-5ddc-493a-b9f8-3bdc548b562e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3146f5a9f3e22753cc86c07b609d997be580b9f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079802"
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>SQL Server 프로파일러를 사용한 Analysis Services 모니터링 소개
  를 사용 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 하 여 인스턴스에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]생성 된 이벤트를 모니터링할 수 있습니다. 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 다음을 수행할 수 있습니다.  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스의 성능을 모니터링합니다.  
  
-   MDX(Multidimensional Expressions) 문을 디버깅합니다.  
  
-   느리게 실행되는 MDX 문을 식별합니다.  
  
-   프로젝트 개발 단계에서 문을 하나씩 검사해 코드가 제대로 작동하는지 확인하는 방식으로 MDX 문을 테스트합니다.  
  
-   프로덕션 시스템에서 이벤트를 캡처하고 테스트 시스템에서 그 이벤트를 재생하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 문제를 해결합니다. 이러한 방식은 프로덕션 시스템을 방해하지 않고 계속 사용하면서 테스트 또는 디버그 하고자 하는 경우에 유용합니다.  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에서 발생하는 작업을 감사하고 검토합니다. 보안 관리자는 감사된 이벤트 중 하나를 볼 수 있습니다. 여기에는 로그인 시도의 성공 또는 실패 여부와 문 및 개체 액세스의 사용 권한에 대한 성공 또는 실패 여부가 포함됩니다.  
  
-   캡처된 이벤트에 대한 데이터를 화면에 표시하거나 이후 분석 또는 재생용으로 파일 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 각 이벤트에 대한 데이터를 캡처하고 저장할 수 있습니다. 데이터를 재생할 때는 저장된 이벤트를 원래 이벤트가 발생한 순서대로 실시간 또는 단계별로 실행할 수 있습니다.  
  
## <a name="using-sql-server-profiler"></a>SQL Server Profiler 사용  
 추적을 만들거나 재생하기 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 역할의 멤버여야 합니다. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 역할의 멤버인 경우 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 시작 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**프로그램 그룹에서** 를 시작할 수 있습니다.  
  
 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용할 때는 다음에 유의하십시오.  
  
-   추적 정의는 CREATE 문을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 저장됩니다.  
  
-   동시에 여러 추적을 실행할 수 있습니다.  
  
-   동일 추적으로부터 여러 연결이 이벤트를 수신할 수 있습니다.  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 중지하고 다시 시작하면 추적을 계속할 수 있습니다.  
  
    > [!NOTE]  
    >  암호는 추적 이벤트에 표시 되지 않지만 이벤트에서로 \* \* \* \* \* \* 바뀝니다.  
  
 최적의 성능을 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 가장 관심 있는 이벤트만 모니터링하십시오. 너무 많은 이벤트를 모니터링하면 오버헤드가 발생하며 특히 장기간 모니터링을 수행할 경우 추적 파일이나 테이블이 너무 커질 수 있습니다. 또한 수집된 데이터 양을 제한하고 추적이 너무 커지지 않도록 방지하기 위해 필터링을 사용하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 추적 이벤트](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [재생 &#40;Analysis Services&#41;에 대 한 프로파일러 추적을 만듭니다.](create-profiler-traces-for-replay-analysis-services.md)  
  
  
