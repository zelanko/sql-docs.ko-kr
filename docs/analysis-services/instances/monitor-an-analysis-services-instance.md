---
title: Analysis Services 인스턴스 개요 모니터링 | Microsoft Docs
ms.date: 11/16/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39cc5a22165d07aafce29e4216548c4e8d226892
ms.sourcegitcommit: b51edbe07a0a2fdb5f74b5874771042400baf919
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2019
ms.locfileid: "55087632"
---
# <a name="monitoring-overview"></a>모니터링 개요
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services 모니터링 하 고 서버 성능을 튜닝 하는 데 다양 한 도구에 있습니다. 도구를 선택하는 기준은 수행된 모니터링 또는 튜닝 유형과 모니터링할 이벤트에 따라 결정됩니다.

SQL Server Analysis Services를 모니터링 하는 방법에 대 한 자세한 내용은 참조는 [SQL Server 2008 R2 작업 가이드](http://go.microsoft.com/fwlink/?LinkID=225539)합니다.  
  
## <a name="monitoring-tools"></a>모니터링 도구  

|도구  |Description  |
|---------|---------|
|[SQL Server 프로파일러](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)      |   엔진 프로세스 이벤트를 추적 합니다. 또한 서버와 데이터베이스 작업을 모니터링할 수 있습니다 이러한 이벤트에 대 한 데이터를 캡처합니다.      |
| [확장 이벤트](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)     |   경량 추적 및 성능 매우 적은 시스템 리소스를 사용 하는 시스템을 모니터링, 테스트 및 프로덕션 서버에서 문제를 진단 하는 데 이상적인 도구입니다.       |
| [동적 관리 뷰 &#40;Dmv&#41;](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)      |   모델 개체, 서버 작업 및 서버 상태에 대 한 정보를 반환 하는 쿼리. SQL 기반 쿼리는 스키마 행 집합에는 인터페이스입니다.      |
| [추적 이벤트](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)     |  캡처하고 다음 인스턴스에 의해 생성 된 추적 이벤트를 분석 하 여 인스턴스 작업을 수행 합니다. 추적 이벤트는 관련된 추적 이벤트를 더 쉽게 찾을 수 있도록 그룹화되어 있습니다.        |
|   [성능 카운터](../../analysis-services/instances/performance-counters-ssas.md)\*    |    성능 모니터를 사용하면 성능 카운터를 사용하여 Microsoft SQL SSAS(Server Analysis Services) 인스턴스의 성능을 모니터링할 수 있습니다.     |
|[로그 작업](../../analysis-services/instances/performance-counters-ssas.md)\*|SQL Server Analysis Services 인스턴스를 설치한 각 인스턴스마다 하나씩 msmdsrv.log 파일에 서버 알림, 오류 및 경고가 로깅됩니다. |

\* SQL Server Analysis Services만 적용 됩니다.

## <a name="see-also"></a>참고자료

[Azure Analysis Services 서버 메트릭 모니터링](https://docs.microsoft.com/azure/analysis-services/analysis-services-monitor)   
[Azure Analysis Services에 대 한 진단 로깅 설정](https://docs.microsoft.com/azure/analysis-services/analysis-services-logging)
