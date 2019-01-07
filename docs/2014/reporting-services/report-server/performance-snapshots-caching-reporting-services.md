---
title: 성능, 스냅숏, 캐시(Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c578e5e56d575f3d324d8585f73a9891b2ad00ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091683"
---
# <a name="performance-snapshots-caching-reporting-services"></a>성능, 스냅숏, 캐시(Reporting Services)
  보고서 서버 성능은 하드웨어, 보고서에 액세스하는 동시 사용자 수, 보고서의 데이터 양, 출력 형식 등을 비롯한 여러 요소 조합의 영향을 받습니다. 설치와 관련된 성능 요소를 이해하고 원하는 결과를 생성하는 해결 방법을 찾으려면 기준선 데이터를 얻고 테스트를 실행해야 합니다. 도구 및 지침에 대한 자세한 내용은 MSDN의 [Reporting Services 성능 최적화](http://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx) 및 [Visual Studio 2005를 사용한 SQL Server 2005 Reporting Services 보고서 서버의 부하 테스트 수행](http://go.microsoft.com/fwlink/?LinkID=77519)을 참조하세요.  
  
 고려해야 할 일반 원칙은 다음과 같습니다.  
  
-   보고서 처리 및 렌더링은 메모리를 많이 사용하는 작업입니다. 가능하면 메모리가 많은 컴퓨터를 선택합니다.  
  
-   별도의 컴퓨터에 보고서 서버 및 보고서 서버 데이터베이스를 호스팅하는 것이 단일 고성능 컴퓨터에 두 구성 요소를 모두 호스팅하는 것보다 성능이 좋습니다.  
  
-   모든 보고서가 느리게 처리되는 경우 여러 보고서 서버 인스턴스가 단일 보고서 서버 데이터베이스를 지원하는 스케일 아웃 배포를 사용해 보세요. 최상의 결과를 얻으려면 부하 분산 소프트웨어를 사용하여 배포에 요청을 균등하게 분산합니다.  
  
-   단일 보고서가 느리게 처리되는 중이며 보고서를 요청 시 실행해야 하는 경우 보고서 데이터 세트 쿼리를 튜닝합니다. 또한 캐시할 수 있는 공유 데이터 세트를 사용하거나 보고서를 캐시하거나 보고서를 스냅숏으로 실행하는 것을 고려할 수도 있습니다.  
  
-   PDF로 렌더링할 때처럼 모든 보고서가 특정 형식에서 느리게 처리되는 경우 파일 공유 배달을 사용하거나 메모리를 추가하거나 다른 형식을 선택해 보십시오.  
  
-   보고서 및 기타 사용 메트릭을 처리하는 데 소요되는 시간을 확인하려면 보고서 서버 실행 로그를 검토합니다. 자세한 내용은 [보고서 서버 실행 로그 및 ExecutionLog3 뷰](report-server-executionlog-and-the-executionlog3-view.md)합니다.  
  
-   메모리 관리 구성 설정을 조정 하 여 성능 문제를 완화 하는 방법에 대 한 자세한 내용은 참조 하십시오 [보고서 서버 응용 프로그램에 대 한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [보고서 서버 성능 모니터링](monitoring-report-server-performance.md)  
 서버의 처리 부하를 추적하는 데 사용할 수 있는 성능 개체에 대해 설명합니다.  
  
 [보고서 처리 속성 설정](set-report-processing-properties.md)  
 보고서가 요청 시 실행되거나 캐시에서 실행되거나 일정에 따라 보고서 스냅숏으로 실행되도록 구성하는 방법에 대해 설명합니다.  
  
 [보고서 서버 응용 프로그램을 위한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)  
 기본 메모리 관리 동작을 재정의하는 방법에 대해 설명합니다.  
  
 [보고서 캐시 &#40;SSRS&#41;](caching-reports-ssrs.md)  
 보고서 서버의 보고서 캐시 동작에 대해 설명합니다.  
  
 [공유 데이터 집합 캐시 &#40;SSRS&#41;](cache-shared-datasets-ssrs.md)  
 보고서 서버의 공유 데이터 세트 캐싱 동작에 대해 설명합니다.  
  
 [큰 보고서 처리](process-large-reports.md)  
 대형 보고서를 구성 및 배포하는 권장 방법을 제공합니다.  
  
 [보고서 및 공유 데이터 집합 처리에 대 한 제한 시간 값 설정 &#40;SSRS&#41;](setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 쿼리 및 보고서 처리에 대한 제한 시간을 설정하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [실행 중인 프로세스 관리](../subscriptions/manage-a-running-process.md)   
 [보고서 실행 확인](verifying-a-report-run.md)  
  
  
