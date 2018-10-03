---
title: Integration Services 서버용 보고서 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 224345a2dc32f12e925a6f97299c91a5e2f7e9b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096173"
---
# <a name="reports-for-the-integration-services-server"></a>Integration Services 서버를 위한 보고서
  현재 릴리스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], 표준 보고서를 사용할 수 있습니다 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 모니터링 하는 데 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에 배포 된 프로젝트는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버. 이러한 보고서는 패키지 상태 및 기록을 보고 필요한 경우 패키지 실행 실패 원인을 파악하는 데 도움이 됩니다.  
  
 각 보고서 페이지의 위쪽에서 뒤로 아이콘을 클릭하면 확인한 이전 페이지로 이동하고, 새로 고침 아이콘을 클릭하면 페이지에 표시된 정보가 새로 고쳐지며, 인쇄 아이콘을 사용하면 현재 페이지를 인쇄할 수 있습니다.  
  
 패키지를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포하는 방법은 [Integration Services 서버에 프로젝트 배포](../../2014/integration-services/deploy-projects-to-integration-services-server.md)를 참조하세요.  
  
## <a name="integration-services-dashboard"></a>통합 서비스 대시보드  
 **Integration Services 대시보드** 보고서에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 모든 패키지 실행에 대한 개요를 제공합니다. 대시보드에서는 서버에서 실행된 각 패키지를 "확대"하여 발생했을 수 있는 패키지 실행 오류에 대한 특정 세부 정보를 찾을 수 있습니다.  
  
 보고서에는 다음과 같은 정보 섹션이 표시됩니다.  
  
|섹션|Description|  
|-------------|-----------------|  
|**실행 정보**|지난 24시간 동안 서로 다른 상태의 여러 실행 개수를 보여 줍니다(실패, 실행 중, 성공 등).|  
|**패키지 정보**|지난 24시간 동안 실행된 총 패키지 수를 보여 줍니다.|  
|**연결 정보**|지난 24시간 동안 실패한 실행에 사용된 연결을 보여 줍니다.|  
|**패키지 세부 정보**|지난 24시간 동안 발생한 완료된 실행에 대한 세부 정보를 보여 줍니다. 예를 들어 이 섹션에서는 실패한 실행 수, 총 실행 수, 실행 기간(초), 과거 3개월 동안의 평균 실행 기간을 보여 줍니다.<br /><br /> **개요**, **모든 메시지**및 **실행 성능**을 클릭하면 패키지에 대한 추가 정보를 볼 수 있습니다.<br /><br /> **실행 성능** 보고서에서는 마지막 실행 인스턴스의 기간뿐 아니라 시각 및 종료 시간과 적용된 환경도 보여 줍니다.<br /><br /> **실행 성능** 보고서에 포함된 차트 및 연결된 테이블에서는 지난 10개의 성공한 패키지 실행 기간을 보여 줍니다. 또한 이 테이블에서는 3개월 동안의 평균 실행 기간도 보여 줍니다. 이러한 10개의 성공한 패키지 실행에는 런타임에 서로 다른 환경 및 리터럴 값이 적용되었을 수 있습니다.<br /><br /> 끝으로 **실행 성능** 보고서에는 패키지 데이터 흐름 구성 요소의 활성 시간 및 총 시간이 표시됩니다. 활성 시간은 모든 단계에서 구성 요소가 실행하는 데 걸린 총 시간을 의미하고, 총 시간은 구성 요소에 대해 경과된 총 시간을 의미합니다. 이 보고서에는 마지막 패키지 실행의 로깅 수준이 성능 또는 자세히로 설정된 경우 패키지 구성 요소에 대해 이 정보만 표시됩니다.<br /><br /> **개요** 보고서에는 패키지 태스크의 상태가 표시됩니다. **메시지** 보고서에는 패키지 및 태스크(예: 시작 및 종료 시간과 작성된 행 수 보고)에 대한 모든 이벤트 메시지 및 오류 메시지가 표시됩니다.<br /><br /> **개요** 보고서에서 **메시지 보기** 를 클릭하여 **메시지** 보고서로 이동할 수도 있습니다. **메시지** 보고서에서 **개요 보기** 를 클릭하여 **개요** 보고서로 이동할 수도 있습니다.|  
  
 **필터** 를 클릭한 다음 **필터 설정** 대화 상자에서 조건을 선택하여 페이지에 표시되는 테이블을 필터링할 수 있습니다. 사용 가능한 필터 조건은 표시되고 있는 데이터에 따라 달라집니다. **필터 설정** 대화 상자에서 정렬 아이콘을 클릭하여 보고서의 정렬 순서를 변경할 수 있습니다.  
  
## <a name="all-executions-report"></a>모든 실행 보고서  
 **모든 실행 보고서** 에는 서버에서 수행된 모든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 실행에 대한 요약 내용이 표시됩니다. 동일한 패키지의 실행이 여러 개 있을 수 있습니다. **Integration Services 대시보드** 보고서와 달리 특정 날짜 범위 동안 시작된 실행을 표시하도록 **모든 실행** 보고서를 구성할 수 있습니다. 날짜 범위는 수 일, 수 개월 또는 수 년으로 지정할 수 있습니다.  
  
 보고서에는 다음과 같은 정보 섹션이 표시됩니다.  
  
|섹션|Description|  
|-------------|-----------------|  
|필터|보고서에 적용된 현재 필터(예: 시작 시간 범위)를 보여 줍니다.|  
|실행 정보|각 패키지 실행의 시작 시간, 종료 시간 및 기간을 보여 줍니다. 패키지 실행 태스크를 사용하여 자식 패키지에 전달된 값과 같이 패키지 실행과 함께 사용된 매개 변수 값의 목록을 볼 수도 있습니다. 매개 변수 목록을 보려면 개요를 클릭합니다.|  
  
 패키지 실행 태스크를 사용하여 자식 패키지에 값을 제공하는 방법에 대한 자세한 내용은 [Execute Package Task](control-flow/execute-package-task.md)를 참조하십시오.  
  
 매개 변수에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 매개 변수](integration-services-ssis-package-and-project-parameters.md)를 참조하세요.  
  
## <a name="all-connections"></a>모든 연결  
 **모든 연결** 보고서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 발생한 실행 및 실패한 연결에 대해 다음 정보를 제공합니다.  
  
 보고서에는 다음과 같은 정보 섹션이 표시됩니다.  
  
|섹션|Description|  
|-------------|-----------------|  
|Assert|보고서에 적용된 현재 필터(예: 지정된 문자열이 있는 연결 및 **마지막으로 실패한 시간** 범위)를 보여 줍니다.<br /><br /> **마지막으로 실패한 시간** 범위를 설정하면 특정 날짜 범위 동안 발생한 연결 실패만 표시됩니다. 날짜 범위는 수 일, 수 개월 또는 수 년으로 지정할 수 있습니다.|  
|설명|연결 문자열, 연결 실패 기간 동안의 실행 수 및 연결이 마지막으로 실패한 날짜를 보여 줍니다.|  
  
## <a name="all-operations-report"></a>모든 작업 보고서  
 **모든 작업 보고서** 에는 패키지 배포, 유효성 검사 및 실행과 기타 관리 작업을 비롯하여 서버에서 수행된 모든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 작업에 대한 요약이 표시됩니다. Integration Services 대시보드를 사용하는 경우와 마찬가지로 테이블에 필터를 적용하여 표시되는 정보를 좁힐 수 있습니다.  
  
## <a name="all-validations-report"></a>모든 유효성 검사 보고서  
 **모든 유효성 검사 보고서** 에는 서버에서 수행된 모든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 유효성 검사에 대한 요약 내용이 표시됩니다. 요약 내용으로는 상태, 시작 시간 및 종료 시간과 같은 각 유효성 검사에 대한 정보가 표시됩니다. 각 요약 항목에는 유효성 검사 중 생성된 메시지에 대한 링크가 포함됩니다. Integration Services 대시보드를 사용하는 경우와 마찬가지로 테이블에 필터를 적용하여 표시되는 정보를 좁힐 수 있습니다.  
  
## <a name="custom-reports"></a>사용자 지정 보고서  
 **Integration Services 카탈로그** 노드 아래의 **SSISDB** [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]카탈로그 노드에 사용자 지정 보고서(.rdl 파일)를 추가할 수 있습니다. 보고서를 추가하기 전에 세 부분으로 이루어진 명명 규칙을 사용하여 원본 테이블과 같은 참조 개체를 정규화하고 있는지 확인합니다. 그렇지 않으면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 오류를 표시합니다. 명명 규칙은 \<데이터베이스>.\<소유자>.\<개체>입니다. 일례로 SSISDB.internal.executions를 들 수 있습니다.  
  
> [!NOTE]  
>  **데이터베이스** 노드 아래의 **SSISDB** 노드에 사용자 지정 보고서를 추가한 경우에는 SSISDB 접두사가 필요하지 않습니다.  
  
 사용자 지정 보고서를 만들고 추가하는 방법은 [Add a Custom Report to Management Studio](../ssms/object/add-a-custom-report-to-management-studio.md)를 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
 [Integration Services 서버용 보고서 보기](../../2014/integration-services/view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>관련 내용  
 [패키지 실행 및 기타 작업 모니터링](performance/monitor-running-packages-and-other-operations.md)  
  
  
