---
title: For Package Execution on the SSIS Server 로깅을 사용 하도록 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47f74d4510b46b984eb58706ff4ac159cb8b1352
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059364"
---
# <a name="enable-logging-for-package-execution-on-the-ssis-server"></a>SSIS 서버에서 패키지 실행에 대한 로깅 설정
  이 절차에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포한 패키지를 실행할 때 패키지의 로깅 수준을 설정하거나 변경하는 방법에 대해 설명합니다. 패키지를 실행할 때 설정하는 로깅 수준에 따라 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 사용하여 구성하는 패키지 로깅이 재정의됩니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md) 을 참조하세요.  
  
 다음 방법 중 하나를 사용하여 로깅 수준을 지정할 수 있습니다. 이 항목에는 첫 번째 방법에 대해 설명합니다.  
  
-   패키지 실행 대화 상자를 사용하여 패키지 실행 인스턴스 구성  
  
-   [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)를 사용하여 실행 인스턴스에 대한 매개 변수 설정  
  
-   새 작업 단계 대화 상자를 사용하여 패키지 실행에 대한 SQL Server 에이전트 작업 구성  
  
### <a name="to-set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>패키지 실행 대화 상자를 사용하여 패키지의 로깅 수준을 설정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 패키지로 이동합니다.  
  
2.  패키지를 마우스 오른쪽 단추로 클릭하고 **실행**을 선택합니다.  
  
3.  **패키지 실행** 대화 상자에서 **고급** 탭을 선택합니다.  
  
4.  **로깅 수준**에서 로깅 수준을 선택합니다. 사용 가능한 값에 대한 설명은 아래 표를 참조하십시오.  
  
5.  다른 모든 패키지 구성을 완료한 다음 **확인** 을 클릭하여 패키지를 실행합니다.  
  
 다음 로깅 수준을 사용할 수 있습니다.  
  
|로깅 수준|Description|  
|-------------------|-----------------|  
|없음|로깅이 해제됩니다. 패키지 실행 상태에만 기록됩니다.|  
|Basic|사용자 지정 이벤트 및 진단 이벤트 외의 모든 이벤트가 기록됩니다. 이것은 기본값입니다.|  
|성능|성능 통계와 OnError 및 OnWarning 이벤트만 기록됩니다.<br /><br /> **실행 성능** 보고서에는 패키지 데이터 흐름 구성 요소의 활성 시간 및 총 시간이 표시됩니다. 이 정보는 마지막 패키지 실행의 로깅 수준이 **성능** 또는 **자세히**로 설정된 경우에 사용할 수 있습니다. 자세한 내용은 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)을(를) 참조하세요.<br /><br /> [catalog.execution_component_phases](/sql/integration-services/system-views/catalog-execution-component-phases) 뷰에는 각 실행 단계의 데이터 흐름 구성 요소에 대한 시작 시간과 종료 시간이 표시됩니다. 이 뷰에서는 패키지 실행의 로깅 수준이 **성능** 또는 **자세히**로 설정된 경우에만 해당 구성 요소에 대해 이 정보를 표시합니다.|  
|자세히|사용자 지정 이벤트 및 진단 이벤트를 포함한 모든 이벤트가 기록됩니다.<br /><br /> 진단 이벤트의 한 예로 DiagnosticEx 이벤트가 있습니다. 이 이벤트는 패키지 실행 태스크가 자식 패키지를 실행할 때마다 기록됩니다. 이 이벤트 메시지는 자식 패키지에 전달된 매개 변수 값으로 구성됩니다.<br /><br /> DiagnosticEx에 대한 메시지 열 값은 XML 텍스트입니다. . 패키지 실행에 대한 메시지 텍스트를 보려면 [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database) 뷰를 쿼리합니다.<br /><br /> 참고: 사용자 지정 이벤트로는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 태스크에 의해 기록되는 이벤트가 있습니다. 자세한 내용은 [Custom Messages for Logging](../../2014/integration-services/custom-messages-for-logging.md)를 참조하세요.<br /><br /> [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) 뷰는 패키지 실행에 대해 데이터 흐름 구성 요소가 다운스트림 구성 요소에 데이터를 전송할 때마다 행을 표시합니다. 뷰에서 이 정보를 캡처하려면 로깅 수준을 **자세히** 로 설정해야 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)   
 [SQL Server Data Tools에서 패키지 로깅 사용](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)  
  
  
