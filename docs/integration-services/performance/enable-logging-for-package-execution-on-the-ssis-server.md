---
title: "SSIS 서버에서 패키지 실행에 대한 로깅 설정 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1"
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# SSIS 서버에서 패키지 실행에 대한 로깅 설정
  이 항목에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 패키지를 실행할 때 패키지의 로깅 수준을 설정하거나 변경하는 방법에 대해 설명합니다. 패키지를 실행할 때 설정하는 로깅 수준에 따라 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 디자인 타임 시 구성하는 패키지 로깅이 재정의됩니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)을 참조하세요.  
  
 SQL Server **서버 속성**의 **서버 로깅 수준** 속성에서 기본 서버 차원의 로깅 수준을 선택할 수 있습니다. 이 항목에서 설명하는 기본 제공 로깅 수준 중 하나에서 선택하거나 기존 사용자 지정된 로깅 수준을 선택할 수 있습니다. 선택한 로깅 수준은 기본적으로 SSIS 카탈로그에 배포되는 모든 패키지에 적용됩니다. 또한 SSIS 패키지를 실행하는 SQL 에이전트 작업 단계에 기본적으로 적용됩니다.  
  
 다음 방법 중 하나를 사용하여 개별 패키지에 대한 로깅 수준을 지정할 수도 있습니다. 이 항목에는 첫 번째 방법에 대해 설명합니다.  
  
-   패키지 실행 대화 상자를 사용하여 패키지 실행 인스턴스 구성  
  
-   [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)를 사용하여 실행 인스턴스에 대한 매개 변수 설정  
  
-   새 작업 단계 대화 상자를 사용하여 패키지 실행에 대한 SQL Server 에이전트 작업 구성  
  
## 패키지 실행 대화 상자를 사용하여 패키지의 로깅 수준 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 패키지로 이동합니다.  
  
2.  패키지를 마우스 오른쪽 단추로 클릭하고 **실행**을 선택합니다.  
  
3.  **패키지 실행** 대화 상자에서 **고급** 탭을 선택합니다.  
  
4.  **로깅 수준**에서 로깅 수준을 선택합니다. 이 항목은 사용 가능한 값에 대한 설명을 포함합니다.  
  
5.  다른 모든 패키지 구성을 완료한 다음 **확인** 을 클릭하여 패키지를 실행합니다.  
  
## 로깅 수준 선택  
 다음 기본 제공 로깅 수준을 사용할 수 있습니다. 또한 기존 사용자 지정된 로깅 수준을 선택할 수 있습니다. 이 항목은 사용자 지정된 로깅 수준에 대한 설명을 포함합니다.  
  
|로깅 수준|Description|  
|-------------------|-----------------|  
|InclusionThresholdSetting|로깅이 해제됩니다. 패키지 실행 상태에만 기록됩니다.|  
|Basic|사용자 지정 이벤트 및 진단 이벤트 외의 모든 이벤트가 기록됩니다. 이 값은 기본값입니다.|  
|RuntimeLineage|데이터 흐름에서 계보 정보를 추적하는 데 필요한 데이터를 수집합니다. 이 계보 정보를 구문 분석하여 작업 간의 계보 관계를 매핑할 수 있습니다. ISV 및 개발자는 이 정보를 사용하여 사용자 지정 계보 매핑 도구를 빌드할 수 있습니다.|  
|성능|성능 통계와 OnError 및 OnWarning 이벤트만 기록됩니다.<br /><br /> **실행 성능** 보고서에는 패키지 데이터 흐름 구성 요소의 활성 시간 및 총 시간이 표시됩니다. 이 정보는 마지막 패키지 실행의 로깅 수준이 **성능** 또는 **자세히**로 설정된 경우에 사용할 수 있습니다. 자세한 내용은 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)을(를) 참조하세요.<br /><br /> [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) 뷰에는 각 실행 단계의 데이터 흐름 구성 요소에 대한 시작 시간과 종료 시간이 표시됩니다. 이 뷰에서는 패키지 실행의 로깅 수준이 **성능** 또는 **자세히**로 설정된 경우에만 해당 구성 요소에 대해 이 정보를 표시합니다.|  
|자세히|사용자 지정 이벤트 및 진단 이벤트를 포함한 모든 이벤트가 기록됩니다.<br /><br /> 사용자 지정 이벤트로는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 태스크에 의해 기록되는 이벤트가 있습니다. 사용자 지정 이벤트에 대한 자세한 내용은 [Custom Messages for Logging](../../integration-services/performance/custom-messages-for-logging.md)을(를) 참조하세요.<br /><br /> 진단 이벤트의 한 예로 **DiagnosticEx** 이벤트가 있습니다. 패키지 실행 태스크가 자식 패키지를 실행할 때마다 이 이벤트는 자식 패키지에 전달된 매개 변수 값을 캡처합니다.<br /><br /> 또한 **DiagnosticEx** 이벤트는 행 수준 오류가 발생하는 열의 이름을 가져올 수 있습니다. 이 이벤트는 로그에 데이터 흐름 계보 지도를 작성합니다. 그런 다음 오류 출력에 의해 캡처된 열 식별자를 사용하여 이 계보 맵에서 열 이름을 조회할 수 있습니다.  자세한 내용은 [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md)를 참조하십시오.<br /><br /> **DiagnosticEx** 에 대한 메시지 열 값은 XML 텍스트입니다. 패키지 실행에 대한 메시지 텍스트를 보려면 [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) 뷰를 쿼리합니다. **DiagnosticEx** 이벤트는 로그의 크기를 줄이기 위해 해당 XML 출력에서 공백을 유지하지 않습니다. 가독성을 높이기 위해 XML 서식 지정 및 구문 강조를 지원하는 XML 편집기(예: Visual Studio)로 로그를 복사합니다.<br /><br /> [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) 뷰는 패키지 실행에 대해 데이터 흐름 구성 요소가 다운스트림 구성 요소에 데이터를 전송할 때마다 행을 표시합니다. 뷰에서 이 정보를 캡처하려면 로깅 수준을 **자세히** 로 설정해야 합니다.|  
  
## 사용자 지정된 로깅 수준 관리 대화 상자를 사용하여 사용자 지정된 로깅 수준 만들기 및 관리  
 원하는 통계 및 이벤트를 수집하는 사용자 지정된 로깅 수준을 만들 수 있습니다. 필요에 따라 변수 값, 연결 문자열 및 구성 요소 속성을 포함하는 이벤트의 컨텍스트를 캡처할 수도 있습니다. 패키지를 실행하는 경우 기본 제공 로깅 수준을 선택할 수 있을 때마다 사용자 지정된 로깅 수준을 선택할 수 있습니다.  
  
> [!TIP]  
>  패키지 변수 값을 캡처하려면 변수의 **IncludeInDebugDump** 속성을 **True**로 설정해야 합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용자 지정된 로깅 수준을 만들고 관리하려면 SSISDB 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **사용자 지정된 로깅 수준**을 선택하여 **사용자 지정된 로깅 수준 관리** 대화 상자를 엽니다. **사용자 지정된 로깅 수준** 목록은 모든 기존 사용자 지정된 로깅 수준을 포함합니다.  
  
2.  새 사용자 지정된 로깅 수준을 **만들려면** **만들기**를 클릭한 다음 이름 및 설명을 제공합니다. **통계** 및 **이벤트** 탭에서 수집하려는 통계 및 이벤트를 선택합니다. **이벤트** 탭에서 필요에 따라 개별 이벤트에 **컨텍스트 포함** 을 선택합니다. 그런 다음 **저장**을 클릭합니다.  
  
3.  기존 사용자 지정된 로깅 수준을 **업데이트** 하려면 목록에서 선택하고 다시 구성한 다음 **저장**을 클릭합니다.  
  
4.  기존 사용자 지정된 로깅 수준을 **삭제** 하려면 목록에서 선택한 다음 **삭제**를 클릭합니다.  
  
 **사용자 지정된 로깅 수준에 대한 권한.**  
  
-   SSISDB 데이터베이스의 모든 사용자는 사용자 지정된 로깅 수준을 보고 패키지를 실행할 때 사용자 지정된 로깅 수준을 선택할 수 있습니다.  
  
-   ssis_admin 또는 sysadmin 역할의 사용자만 사용자 지정된 로깅 수준을 만들고 업데이트 또는 삭제할 수 있습니다.  
  
## 관련 항목:  
 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)   
 [SQL Server Data Tools에서 패키지 로깅 설정](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)  
  
  