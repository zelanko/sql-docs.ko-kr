---
title: DQS 관리 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8bd848acf0dc8c45c1aacf884219421a6309ecd5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dqs-administration"></a>dqs 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  DQS([!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )를 사용하면 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에서 수행되는 여러 DQS 활동을 관리하고, DQS 활동과 관련된 서버 수준의 속성을 구성하고, 참조 데이터 서비스 설정을 구성하고, DQS 로그 설정을 구성할 수 있습니다. 이러한 작업은 **의** 관리 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]기능을 통해 수행됩니다. DQS의 보안 액세스(역할)에 따라 사용자에게는 이 영역의 특정 기능에 대한 액세스 권한이 부여되거나 거부됩니다.  
  
 이러한 관리 활동과 별도로 이 항목에서는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]를 사용하여 수행되지 않는 관리 활동, DQS 데이터베이스 백업 및 복원에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 의 관리 기능에는 다음과 같은 이점이 있습니다.  
  
-   관리자가 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]의 여러 DQS 활동을 모니터링할 수 있습니다.  
  
-   DQS 관리자가 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]의 DQS 활동을 모니터링하고, 필요에 따라 실행 중인 활동을 *종료* 하거나 활동 내에서 실행 중인 프로세스를 *중지* 할 수 있습니다.  
  
-   Windows Azure Marketplace와의 연결을 설정하고 직접 타사 참조 데이터 서비스 공급자를 관리하는 등의 참조 데이터 서비스 설정을 구성합니다.  
  
-   정리 및 일치 활동에 대한 임계값을 구성합니다.  
  
-   [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 알림을 설정/해제합니다.  
  
-   이벤트의 심각도 수준에 따라 로깅을 구성합니다.  
  
##  <a name="AdminUsingClent"></a> Data Quality 클라이언트를 사용한 관리 활동  
 이러한 활동은 **의** 관리 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]기능을 사용하여 수행됩니다.  
  
### <a name="activity-monitoring"></a>작업 모니터링  
 **의** 활동 모니터링 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 에는 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에서 수행되는 각 활동에 대한 자세한 정보를 표시합니다. 이 화면은 데이터 관리자가 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 응용 프로그램이 연결된 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 에서 수행되는 모든 작업에 대한 상위 수준의 모니터링을 수행하는 데 주로 사용됩니다. 이 화면에서는 시스템 수준 모니터링을 제공하지 않습니다. 또한 이 화면에서 DQS 관리자는 필요에 따라 실행 중인 활동을 종료하거나 활동 내에서 실행 중인 프로세스를 중지하여 활동 또는 활동 내의 프로세스를 제어할 수 있습니다. 데이터는 기술 자료 검색, 도메인 관리, 일치 정책, 정리, 일치, SSIS(SQL Server Integration Services) 기반 정리에 대해 표시됩니다.  
  
### <a name="configuration"></a>Configuration  
 **의** 구성 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 화면에서는 DQS 관리자가 다음 작업을 수행할 수 있습니다.  
  
-   **참조 데이터**: 참조 데이터 서비스 공급자 구성: Windows Azure 마켓플레이스 또는 다이렉트 참조 데이터 서비스 공급자입니다. 참조 데이터 서비스 공급자를 설정한 후 기술 자료에서 도메인 관리 활동 중 참조 데이터와 함께 도메인/복합 도메인을 매핑하고 동일한 기술 자료를 데이터 품질 프로젝트의 정리 활동에 대해 사용할 수 있습니다. 또한 Windows Azure Marketplace를 사용하도록 인터넷에 연결하기 위해 프록시 설정을 지정할 수 있습니다.  
  
-   **일반 설정**: 데이터 정리 및 데이터 일치에 대한 임계값을 지정하고 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 프로파일링을 위한 알림을 사용하도록 설정할지 여부를 지정합니다. 이러한 임계값은 데이터 품질 프로젝트에서 컴퓨터 기반 정리 및 일치 활동 중에 DQS에서 사용됩니다.  
  
-   **로그 설정**: DQS의 로그 파일은 DQS에서 수행되는 활동을 기록하며 유지 관리 및 문제 해결 중 작업 문제를 추적하는 데 유용합니다. 이벤트 심각도 수준에 따라 다양한 DQS 기능(도메인 관리, 기술 자료 검색, 정리, 일치 및 참조 데이터 서비스) 및 DQS 모듈에 대해 기록하려는 메시지를 필터링할 수 있습니다.  
  
> [!NOTE]  
>  **구성** 화면은 DQS_MAIN 데이터베이스에서 dqs_administrator 역할이 있는 사용자에게만 제공됩니다.  
  
##  <a name="AdminOutsideClient"></a> Data Quality 클라이언트 외부의 관리 활동  
 다음 활동은 Data Quality 클라이언트 외부에서 수행됩니다.  
  
-   **DQS 데이터베이스 백업 및 복원**: DQS 데이터베이스의 백업 및 복원은 DQS와 관련된 몇 가지 고려 사항을 제외하면 다른 SQL Server 데이터베이스를 백업 및 복원하는 것과 동일합니다.  
  
-   **DQS 데이터베이스 분리 및 연결**: DQS 데이터베이스를 분리 및 연결하는 단계는 DQS와 관련된 몇 가지 고려 사항을 제외하면 다른 SQL Server 데이터베이스를 분리 및 연결하는 단계와 동일합니다.  
  
 자세한 내용은 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|DQS에서 활동을 모니터링하는 방법을 설명합니다.|[DQS 작업 모니터링](../data-quality-services/monitor-dqs-activities.md)|  
|DQS에서 참조 데이터 설정을 구성하는 방법을 설명합니다.|[참조 데이터를 사용하도록 DQS 구성](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|정리 및 일치 활동을 위한 임계값 구성 방법을 설명합니다.|[정리 및 일치에 대한 임계값 구성](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|DQS에서 알림을 설정 또는 해제하는 방법에 대해 설명합니다.|[DQS에서 프로파일링 알림 설정 또는 해제](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|이벤트의 심각도 수준에 따라 DQS 로깅을 구성하는 방법을 설명합니다.|[DQS 로그 파일에 대한 심각도 수준 구성](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|DQS 로깅에 대한 고급 설정을 구성하는 방법을 설명합니다.|[DQS 로그 파일에 대한 고급 설정 구성](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|DQS 데이터베이스를 백업 및 복원하는 방법을 설명합니다.|[DQS 데이터베이스 백업 및 복원](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|DQS 데이터베이스를 분리하고 연결하는 방법을 설명합니다.|[DQS 데이터베이스 분리 및 연결](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>참고 항목  
 [DQS의 참조 데이터 서비스](../data-quality-services/reference-data-services-in-dqs.md)   
 [DQS 로그 파일 관리](../data-quality-services/manage-dqs-log-files.md)   
 [DQS 데이터베이스 관리](../data-quality-services/manage-dqs-databases.md)  
  
  
