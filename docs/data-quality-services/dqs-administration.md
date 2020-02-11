---
title: dqs 관리
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 065a8869eff0e88cee5bf0bb110a948f709743d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75251665"
---
# <a name="dqs-administration"></a>dqs 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]DQS ()를 사용 하면에서 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]수행 되는 여러 dqs 활동을 관리 하 고, dqs 활동과 관련 된 서버 수준 속성을 구성 하 고, 참조 데이터 서비스 설정을 구성 하 고, dqs 로그 설정을 구성할 수 있습니다. 이러한 작업은 **의** 관리 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]기능을 통해 수행됩니다. DQS의 보안 액세스(역할)에 따라 사용자에게는 이 영역의 특정 기능에 대한 액세스 권한이 부여되거나 거부됩니다.  
  
 이러한 관리 활동과 별도로 이 항목에서는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]를 사용하여 수행되지 않는 관리 활동, DQS 데이터베이스 백업 및 복원에 대한 정보를 제공합니다.  
  
 
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 의 관리 기능에는 다음과 같은 이점이 있습니다.  
  
-   관리자가 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]의 여러 DQS 활동을 모니터링할 수 있습니다.  
  
-   DQS 관리자가 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]의 DQS 활동을 모니터링하고, 필요에 따라 실행 중인 활동을 *종료* 하거나 활동 내에서 실행 중인 프로세스를 *중지* 할 수 있습니다.  
  
-   Azure Marketplace 연결 설정 및 직접 타사 참조 데이터 서비스 공급자 관리와 같은 참조 데이터 서비스 설정을 구성 합니다.  
  
-   정리 및 일치 활동에 대한 임계값을 구성합니다.  
  
-   
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 알림을 설정/해제합니다.  
  
-   이벤트의 심각도 수준에 따라 로깅을 구성합니다.  
  
##  <a name="AdminUsingClent"></a>Data Quality Client를 사용한 관리 활동  
 이러한 활동은 **의** 관리 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]기능을 사용하여 수행됩니다.  
  
### <a name="activity-monitoring"></a>작업 모니터링  
 
  **의** 활동 모니터링 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 에는 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에서 수행되는 각 활동에 대한 자세한 정보를 표시합니다. 이 화면은 데이터 관리자가 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 애플리케이션이 연결된 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 에서 수행되는 모든 작업에 대한 상위 수준의 모니터링을 수행하는 데 주로 사용됩니다. 이 화면에서는 시스템 수준 모니터링을 제공하지 않습니다. 또한 이 화면에서 DQS 관리자는 필요에 따라 실행 중인 활동을 종료하거나 활동 내에서 실행 중인 프로세스를 중지하여 활동 또는 활동 내의 프로세스를 제어할 수 있습니다. 데이터는 기술 자료 검색, 도메인 관리, 일치 정책, 정리, 일치, SSIS(SQL Server Integration Services) 기반 정리에 대해 표시됩니다.  
  
### <a name="configuration"></a>구성  
 
  **의** 구성 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 화면에서는 DQS 관리자가 다음 작업을 수행할 수 있습니다.  
  
-   **참조 데이터**: 참조 데이터 서비스 공급자 구성: Azure Marketplace 또는 다이렉트 참조 데이터 서비스 공급자입니다. 참조 데이터 서비스 공급자를 설정한 후 기술 자료에서 도메인 관리 활동 중 참조 데이터와 함께 도메인/복합 도메인을 매핑하고 동일한 기술 자료를 데이터 품질 프로젝트의 정리 활동에 대해 사용할 수 있습니다. 또한 Azure Marketplace를 사용 하기 위해 인터넷에 연결 하기 위한 프록시 설정을 지정할 수 있습니다.  
  
-   **일반 설정**: 데이터 정리 및 데이터 일치에 대 한 임계값과에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]프로 파일링에 대 한 알림을 사용할지 여부를 지정 합니다. 이러한 임계값은 데이터 품질 프로젝트에서 컴퓨터 기반 정리 및 일치 활동 중에 DQS에서 사용됩니다.  
  
-   **로그 설정**: dqs의 로그 파일은 dqs에서 수행 되는 활동을 기록 하며 유지 관리 및 문제 해결 중에 운영 문제를 추적 하는 데 유용 합니다. 이벤트 심각도 수준에 따라 다양한 DQS 기능(도메인 관리, 기술 자료 검색, 정리, 일치 및 참조 데이터 서비스) 및 DQS 모듈에 대해 기록하려는 메시지를 필터링할 수 있습니다.  
  
> [!NOTE]  
>  
  **구성** 화면은 DQS_MAIN 데이터베이스에서 dqs_administrator 역할이 있는 사용자에게만 제공됩니다.  
  
##  <a name="AdminOutsideClient"></a>Data Quality Client 외부의 관리 활동  
 다음 활동은 Data Quality 클라이언트 외부에서 수행됩니다.  
  
-   
  **DQS 데이터베이스 백업 및 복원**: DQS 데이터베이스의 백업 및 복원은 DQS와 관련된 몇 가지 고려 사항을 제외하면 다른 SQL Server 데이터베이스를 백업 및 복원하는 것과 동일합니다.  
  
-   **Dqs 데이터베이스 분리 및 연결**: dqs 데이터베이스를 분리 하 고 연결 하는 단계는 dqs와 관련 된 몇 가지 고려 사항으로 SQL Server 데이터베이스를 분리 하 고 연결 하는 단계와 동일 합니다.  
  
 자세한 내용은 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|DQS에서 활동을 모니터링하는 방법을 설명합니다.|[DQS 작업 모니터링](../data-quality-services/monitor-dqs-activities.md)|  
|DQS에서 참조 데이터 설정을 구성하는 방법을 설명합니다.|[참조 데이터를 사용하도록 DQS 구성](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|정리 및 일치 활동을 위한 임계값 구성 방법을 설명합니다.|[정리 및 일치에 대한 임계값 구성](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|DQS에서 알림을 설정 또는 해제하는 방법에 대해 설명합니다.|[DQS에서 프로파일링 알림 설정 또는 해제](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|이벤트의 심각도 수준에 따라 DQS 로깅을 구성하는 방법을 설명합니다.|[DQS 로그 파일에 대한 심각도 수준 구성](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|DQS 로깅에 대한 고급 설정을 구성하는 방법을 설명합니다.|[Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|DQS 데이터베이스를 백업 및 복원하는 방법을 설명합니다.|[DQS 데이터베이스 백업 및 복원](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|DQS 데이터베이스를 분리하고 연결하는 방법을 설명합니다.|[DQS 데이터베이스 분리 및 연결](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>참고 항목  
 [DQS의 참조 Data Services](../data-quality-services/reference-data-services-in-dqs.md)   
 [DQS 로그 파일 관리](../data-quality-services/manage-dqs-log-files.md)   
 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)  
  
  
