---
title: 보고서 및 공유 데이터 집합 처리에 대한 시간 제한 값 설정(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- time-outs [Reporting Services]
- query time-outs [Reporting Services]
- report processing [Reporting Services], time-outs
- report execution time-outs [Reporting Services]
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
caps.latest.revision: 38
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4794c4a2b6c9207cb48573bb481499fa402f3b29
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37214573"
---
# <a name="setting-time-out-values-for-report-and-shared-dataset-processing-ssrs"></a>보고서 및 공유 데이터 집합 처리에 대한 제한 시간 값 설정(SSRS)
  제한 시간 값을 지정하여 시스템 리소스 사용 방식에 대해 제한을 설정할 수 있습니다. 보고서 서버는 다음 두 가지 제한 시간 값을 지원합니다.  
  
-   포함된 데이터 집합 쿼리 제한 시간 값은 보고서 서버가 데이터베이스의 응답을 기다리는 시간(초)입니다. 이 값은 보고서에서 정의됩니다.  
  
-   공유 데이터 집합 쿼리 제한 시간 값은 보고서 서버가 데이터베이스의 응답을 기다리는 시간(초)입니다. 이 값은 공유 데이터 집합 정의의 일부이며 보고서 서버에서 공유 데이터 집합을 관리할 때 변경될 수 있습니다.  
  
-   보고서 실행 제한 시간 값은 보고서 처리가 중지되기까지 계속될 수 있는 최대 시간(초)입니다. 이 값은 시스템 수준에서 정의됩니다. 이 설정은 보고서마다 다르게 설정할 수 있습니다.  
  
 대부분의 제한 시간 오류는 쿼리가 처리되는 동안 발생합니다. 제한 시간 오류가 발생하면 쿼리 제한 시간 값을 늘려 보십시오. 보고서 실행 제한 시간 값을 쿼리 제한 시간보다 크게 조정해야 합니다. 시간은 쿼리와 보고서 둘 다를 처리하기에 충분해야 합니다.  
  
## <a name="setting-a-query-time-out-for-an-embedded-dataset-in-a-report"></a>보고서에 포함된 데이터 집합의 쿼리 제한 시간 설정  
 쿼리 제한 시간 값은 보고서를 작성하는 동안 포함된 데이터 집합을 정의할 때 지정됩니다. 시간 제한 값에 보고서와 함께 저장 됩니다는 `Timeout` 보고서 정의의 요소입니다. 기본적으로 이 값은 30초로 설정됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.  
  
 게시된 보고서의 속성을 수정할 권한이 있는 사용자는 보고서 정의 파일을 편집하여 이 값을 다시 설정할 수 있습니다.  
  
 데이터 기반 구독에 대한 쿼리 제한 시간 값도 지정할 수 있습니다. 이 쿼리 제한 시간 값은 데이터 기반 구독 페이지에서 지정합니다. 지정한 값에 따라 구독자 데이터 원본에서 데이터를 검색할 때 보고서 서버에서 쿼리 처리가 완료되기를 기다리는 시간이 결정됩니다.  
  
## <a name="setting-a-query-time-out-for-a-shared-dataset"></a>공유 데이터 집합의 쿼리 제한 시간 설정  
 쿼리 제한 시간 값은 보고서 서버에서 공유 데이터 집합을 만들거나 관리할 때 초 단위로 지정됩니다. 기본적으로 이 값은 0초로 설정되며 이것은 제한 시간 값이 없는 것과 같습니다. 자세한 내용은 [공유 데이터 집합 관리](../report-data/manage-shared-datasets.md)합니다.  
  
## <a name="setting-a-report-execution-time-out"></a>보고서 실행 제한 시간 설정  
 보고서 실행 제한 시간 값을 설정하여 보고서 서버에서 보고서를 처리하는 데 사용하는 시간을 제한할 수 있습니다. 보고서 실행 제한 시간 값은 보고서 관리자에서 지정할 수 있습니다. 사이트 설정 페이지에서 모든 보고서에 대해 기본값을 설정한 다음 특정 보고서에 대한 실행 속성 페이지에서 해당 값을 재정의할 수 있습니다. 기본적으로 이 값은 1800초로 설정되어 있습니다. 자세한 내용은 [보고서 처리 속성 설정](set-report-processing-properties.md)을 참조하세요.  
  
## <a name="how-report-execution-time-out-values-are-evaluated"></a>보고서 실행 제한 시간 값 평가 방법  
 보고서 서버는 60초 간격으로 실행 작업을 평가합니다. 60초마다 실제 처리 시간을 보고서 실행 제한 시간 값과 비교하여 보고서 처리 시간이 보고서 실행 제한 시간 값을 초과하면 보고서 처리가 중지됩니다.  
  
 제한 시간 값을 60초 이내로 지정한 경우 보고서 서버에서 실행 작업을 평가하지 않는 휴지 시간 동안 보고서 처리가 시작되어 완료되면 보고서를 완전하게 실행할 수 있습니다. 예를 들어 실행 시간이 20초인 보고서에 실행 제한 시간 값을 10초로 설정하면 보고서가 60초 주기의 초반에 실행되는 경우 보고서는 완전하게 처리됩니다.  
  
> [!NOTE]  
>  RSReportServer.config 파일에서 `RunningRequestsDbCycle`을 설정하여 실행 작업의 평가 빈도를 변경할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [처리 옵션 설정 &#40;Reporting Services sharepoint에서 통합 모드&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](reporting-services-report-server-native-mode.md)   
 [실행 중인 프로세스 관리](../subscriptions/manage-a-running-process.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)  
  
  
