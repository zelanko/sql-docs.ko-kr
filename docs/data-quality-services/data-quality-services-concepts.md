---
title: "Data Quality Services 개념 | Microsoft Docs"
ms.custom: 
ms.date: 01/01/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 837c71ee-48fa-4044-8744-2be9119aaa04
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 51b4813c67c7f7346bea533764b13fceef06db12
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="data-quality-services-concepts"></a>Data Quality Services 개념
  이 항목에서는 기술 자료 관리, 데이터 품질 프로젝트 및 데이터 품질 관리의 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] ) 개념을 간단히 요약합니다.  
  
##  <a name="Knowledge"></a> 기술 자료 관리 개념  
 DQS 기술 자료는 데이터 관리자나 IT 전문가가 데이터 정리 및 데이터 일치를 통해 데이터 품질 향상을 위해 만든 메타데이터의 리포지토리입니다. DQS 기술 자료 관리에는 컴퓨터 기반은 물론 대화형으로도 기술 자료를 만들고 관리하는 데 사용되는 프로세스가 포함됩니다.  
  
 **기술 자료 검색**  
  
 기술 자료 검색은 조직의 데이터 샘플을 분석하여 데이터에 대한 기술 자료를 구축하는 프로세스입니다. 분석 결과가 나오면 기술 자료의 유효성을 검사하고 개선한 후 데이터 정리, 일치 및 프로파일링을 수행하는 데 적용할 수 있습니다. 자세한 내용은 [DQS Knowledge Bases and Domains](../data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하세요.  
  
 **도메인 관리**  
  
 도메인 관리 프로세스에서는 기술 자료 검색 프로세스에서 생성된 기술 자료를 변경하거나 보강할 수 있습니다. 기술 자료를 대화형으로 편집, 업데이트 및 검토할 수 있습니다. 기술 자료는 도메인 값과 해당 상태, 도메인 규칙, 용어 기반 관계 및 참조 데이터가 포함된 데이터 도메인으로 구성됩니다. 도메인 관리에서 도메인 속성을 변경하고, 참조 데이터를 도메인에 연결하고, 도메인 규칙을 관리하고, 도메인 값을 관리하며 데이터 관계를 입력하고, 도메인을 만들거나 삭제하거나 가져오거나 내보낼 수 있습니다. 둘 이상의 단일 도메인을 집계하는 복합 도메인을 사용할 수도 있습니다. 자세한 내용은 [DQS Knowledge Bases and Domains](../data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하세요.  
  
 **일치 정책**  
  
 일치 정책에는 데이터 중복 제거를 수행하는 데 사용되는 일치 규칙이 포함됩니다. 일치 정책 프로세스에서는 일치 규칙을 만들고, 일치 결과와 프로파일링 데이터를 기반으로 이 결과를 미세 조정하며, 정책을 기술 자료에 추가할 수 있습니다. 자세한 내용은 [데이터 일치](../data-quality-services/data-matching.md)을 참조하세요.  
  
 **참조 데이터 서비스**  
  
 참조 데이터를 사용하면 참조 데이터 품질을 보장하는 회사의 서비스를 이용하여 데이터의 유효성을 검사하고 데이터를 수정 및 보강할 수 있습니다. Windows Azure Marketplace의 서비스를 사용하여 참조 데이터 공급자에 연결하거나 공급자에 대한 직접 연결을 사용할 수 있습니다. 자세한 내용은 [Reference Data Services in DQS](../data-quality-services/reference-data-services-in-dqs.md)을 참조하세요.  
  
 DQS의 기술 자료 관리에 대한 자세한 내용은 [DQS Knowledge Bases and Domains](../data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하세요.  
  
##  <a name="Projects"></a> 데이터 품질 프로젝트 개념  
 데이터 관리자는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램에서 데이터 품질 프로젝트를 사용하여 데이터 품질 작업(정리 및 일치)을 수행합니다.  
  
 **데이터 정리**  
  
 DQS의 데이터 정리 작업은 DQS 기술 자료의 지식을 기반으로 수행됩니다. DQS의 데이터 정리 작업은 2단계 프로세스입니다.  
  
-   **컴퓨터 기반 정리**: DQS에서는 정리 프로젝트에 대해 선택된 기술 자료의 지식을 사용하여 데이터 원본에 있는 값에 대한 수정/제안 사항을 제공합니다.  
  
-   **대화형 정리**: 데이터 관리자는 대화형 정리 프로세스를 수행하여 컴퓨터 기반 데이터 정리 프로세스에서 제안한 데이터 수정 사항을 변경하거나 보강할 수 있습니다. 데이터 관리자는 데이터 정리 프로세스에서 식별된 신뢰 수준과 통계를 사용하거나 변경 사항을 프로젝트에 수동으로 입력하여 이 작업을 수행합니다.  
  
 데이터 관리자는 데이터를 정리한 후 처리된 데이터를 SQL Server 데이터베이스, .csv 파일 또는 Excel 파일로 내보낼 수 있습니다. 자세한 내용은 [Data Cleansing](../data-quality-services/data-cleansing.md)을 참조하세요.  
  
 **데이터 일치**  
  
 일치 프로세스에서는 데이터 관리자가 데이터를 비교하여 중복 제거 프로세스를 통해 비슷하지만 약간 다른 데이터를 정렬할 수 있습니다. DQS에서는 기술 자료에 포함된 일치 규칙을 기반으로 중복 제거를 수행합니다. 데이터 관리자는 데이터 품질 프로젝트 내에서 일치 프로세스에 대한 매개 변수를 지정합니다. 자세한 내용은 [데이터 일치](../data-quality-services/data-matching.md)을 참조하세요.  
  
 **프로파일링 및 알림**  
  
 데이터 관리자는 데이터 프로파일링을 통해 DQS에 의해 처리되는 데이터에 대한 실시간 통계 및 정보를 얻어 데이터 품질 프로젝트를 실행하는 동안 정리 또는 일치 작업을 수행할 수 있습니다. 데이터 프로파일링을 활용하면 데이터 품질 프로젝트에서 정리 및 일치 작업의 효과를 평가하는 데 도움이 되며, 알림을 활용하면 사용자가 데이터 정리 및 데이터 일치 작업을 개선하기 위해 취할 수 있는 조치에 도움이 됩니다. 자세한 내용은 [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md)을 참조하세요.  
  
 DQS의 데이터 품질 프로젝트에 대한 자세한 내용은 [데이터 품질 프로젝트&#40;DQS&#41;](../data-quality-services/data-quality-projects-dqs.md)를 참조하세요.  
  
##  <a name="Admin"></a> 데이터 품질 관리 개념  
 DQS 관리자는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램을 사용하여 다양한 관리 태스크를 수행할 수 있습니다.  
  
 **작업 모니터링**  
  
 작업 모니터링은 데이터 범위 내에서 수행한 각 작업의 상태를 표시하고, 각 작업의 데이터를 제공하며, DQS 관리자가 작업을 제어할 수 있도록 합니다. 자세한 내용은 [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md)을 참조하세요.  
  
 **Configuration**  
  
 구성 옵션을 사용하면 다음 작업을 수행할 수 있습니다.  
  
-   참조 데이터 서비스 설정 구성. 자세한 내용은 [Configure DQS to Use Reference Data](../data-quality-services/configure-dqs-to-use-reference-data.md)을 참조하세요.  
  
-   정리 및 일치 작업에 대한 임계값 설정. 자세한 내용은 [정리 및 일치에 대한 임계값 구성](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)을 참조하세요.  
  
-   프로파일링 알림 설정/해제. 자세한 내용은 [DQS에서 프로파일링 알림 설정 또는 해제](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)를 참조하세요.  
  
-   작업 기반 수준이나 고급 모듈 기반 수준에서 DQS 로그 파일에 대한 심각도 수준 구성. 자세한 내용은 [Configure Severity Levels for DQS Log Files](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)을 참조하세요.  
  
 **DQS 보안**  
  
 SQL Server 보안 메커니즘 내의 역할을 사용하여 DQS 보안을 설정할 수 있습니다. [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램에서 사용자의 액세스 수준은 dqs_administrator, dqs_kb_editor 및 dqs_kb_operator라는 세 가지 DQS 역할에 의해 결정됩니다. [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램을 사용하여 사용자에게 역할을 부여할 수는 없습니다. 이 작업은 SQL Server Management Studio를 사용하여 수행됩니다. 자세한 내용은 [DQS Security](../data-quality-services/dqs-security.md)을 참조하세요.  
  
 DQS 관리에 대한 자세한 내용은 [DQS Administration](../data-quality-services/dqs-administration.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Data Quality Services](../data-quality-services/data-quality-services.md)  
  
  
