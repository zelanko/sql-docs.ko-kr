---
title: DQS 로그 파일에 대한 심각도 수준 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.admin.config.log.f1
helpviewer_keywords:
- severity levels
- log files,severity levels
- dqs log files,severity levels
- logging,severity levels
- configure severity levels
ms.assetid: 66ffcdec-4bf7-4dd5-a221-fd9baefeeef4
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b711dfaf089173dcf72f854168e6b73aa05949ab
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937974"
---
# <a name="configure-severity-levels-for-dqs-log-files"></a>DQS 로그 파일에 대한 심각도 수준 구성
  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]를 사용하여 다양한 작업 및 모듈의 심각도를 구성하는 방법에 대해 설명합니다. 심각도는 DQS에서 발생하는 이벤트의 강도를 정의합니다. DQS 이벤트의 심각도는 다음과 같습니다(심각도 내림차순 정렬).  
  
-   **치명적**: 심각한/예기치 않은 결과를 일으킬 수 있는 치명적인 런타임 오류입니다.  
  
-   **오류**: 그 외 런타임 오류입니다.  
  
-   **경고**: 오류를 일으킬 수 있는 이벤트에 대한 경고입니다.  
  
-   **정보**: 오류나 경고가 아닌 일반 이벤트에 대한 정보입니다. 예를 들어 'DQS 프로세스가 시작되었습니다'가 있습니다.  
  
-   **디버그**: 이벤트에 대한 자세한(세부) 정보입니다.  
  
 다양한 DQS 작업 및 모듈의 심각도를 구성하면 해당 DQS 작업 또는 모듈에 대한 DQS 로그 파일에 로깅하고 기록할 정보가 필터링됩니다. 예를 들어 DQS 작업의 심각도를 **경고**로 설정하면 해당 DQS 작업과 관련된 경고 이상의 심각도 메시지만 로깅됩니다(오류 및 치명적).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 로그 심각도 설정을 구성하려면 DQS_MAIN 데이터베이스에 대한 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="configure-severity-levels-at-activity-level"></a><a name="ConfigureActivity"></a>활동 수준에서 심각도 수준 구성  
 DQS에서 도메인 관리, 기술 자료 검색, 일치 정책, 데이터 정리, 데이터 일치 및 참조 데이터 서비스와 같은 작업에 대한 로그 심각도 설정을 구성할 수 있습니다. 이렇게 하려면 다음을 수행합니다.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client 응용 프로그램을 실행](../../2014/data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **구성**을 클릭합니다.  
  
3.  그런 다음 **로그 설정** 탭을 클릭 합니다. 심각도 수준을 선택할 수 있는 DQS 작업 **도메인 관리**, **기술 자료 검색**, **정리 프로젝트 (예: rds)**, **일치 정책 및 일치 프로젝트**및 **RDS**가 나열 됩니다.  
  
4.  특정 DQS 작업에 대해 로깅할 심각도를 선택합니다. 심각도 **치명적**, **오류**, **경고**, **정보**및 **디버그**중 하나를 선택할 수 있습니다. 예를 들어 기술 자료 검색 작업에서 치명적 메시지만 DQS 로그 파일에 기록하려면 **기술 자료 검색** 작업에 대한 드롭다운 목록에서 **치명적** 을 선택합니다.  
  
    > [!NOTE]  
    >  기본적으로 각 작업에 대해 **오류** 가 선택됩니다. 이는 각 작업에 대한 DQS 로그 파일에 기본적으로 오류 및 치명적 메시지가 기록됨을 의미합니다.  
  
5.  **닫기**를 클릭합니다.  
  
##  <a name="configure-severity-levels-at-module-level-advanced"></a><a name="ConfigureModule"></a>모듈 수준에서 심각도 구성 (고급)  
 **로그 설정** 탭의 **고급** 섹션을 사용하여 모듈 수준에서 로그 심각도 설정을 구성할 수 있습니다. 모듈은 DQS의 기능 내에 다양한 기능을 구현하는 DQS 시스템 어셈블리입니다. 예를 들어 도메인 관리 작업에는 도메인 규칙 정의, 규칙 조건 정의, 복합 도메인의 도메인 간 규칙 정의 등과 같은 다양한 기능이 포함됩니다.  
  
 때때로 작업 수준의 세분성 수준으로 충분하지 않은 경우가 있습니다. 한 작업 내 특정 모듈에서 발생한 문제를 조사해야 할 수 있습니다. 그러면 모듈 수준에서 로그 심각도를 구성하여 문제를 더 정확하게 격리하고 추적할 수 있습니다.  
  
 작업 수준에서 지정된 로그 심각도 설정은 작업을 구성하는 모든 모듈의 로그 심각도 설정을 결정합니다. 그러나 작업 수준과 모듈 수준의 로그 심각도 설정에 충돌이 발생한 경우 모듈 수준의 심각도 설정이 고려됩니다.  
  
> [!NOTE]
>  -   기본적으로 **고급** 섹션에 심각도가 **정보** 로 설정된 **Microsoft.Ssdqs.Core.Startup**모듈이 미리 구성되어 있습니다. 이는 DQS 서비스의 시작 및 중지와 관련된 정보 이상의 심각도(경고, 오류 및 치명적) 이벤트에 대한 로깅을 설정하기 위함입니다.  
> -   DQS 시스템 어셈블리에 대해 잘 알고 있는 고급 DQS 사용자인 경우에만 모듈 수준에서 로그 심각도를 구성해야 합니다.  
  
 모듈 수준에서 로그 심각도를 구성하려면  
  
1.  **로그 설정** 탭에서 **고급** 에 대해 아래쪽 화살표를 클릭하여 영역을 표시합니다.  
  
2.  표시된 표에서 **모듈** 열에 있는 드롭다운 목록의 모듈 이름을 선택합니다.  
  
3.  다음으로, **심각도** 열의 드롭다운 목록에서 모듈의 심각도를 선택합니다. 심각도 **치명적**, **오류**, **경고**, **정보**및 **디버그**중 하나를 선택할 수 있습니다.  
  
     예를 들어 도메인 관리 작업 내에서 **Microsoft.Ssdqs.DomainRules.Define** 모듈을 선택하고 다른 로그 심각도를 선택하여 도메인 규칙 정의 기능의 세분성 수준을 도메인 관리 작업과 다르게 설정할 수 있습니다. 마찬가지로 **Microsoft.Ssdqs.DomainRules.Condition.CrossDomain** 모듈을 선택하고 다른 로그 심각도를 선택하여 도메인 간 규칙 기능의 세분성 수준을 다르게 설정할 수 있습니다.  
  
4.  필요한 경우 다른 모듈에 대해 2단계와 3단계를 반복합니다. 또한 **모듈 추가** 및 **모듈 제거** 아이콘을 클릭하여 표에서 행을 추가하거나 삭제할 수도 있습니다.  
  
5.  **닫기**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Configure Advanced Settings for DQS Log Files](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)  
  
  
