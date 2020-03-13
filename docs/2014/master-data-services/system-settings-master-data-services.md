---
title: 시스템 설정(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- Master Data Services, system settings
- system settings [Master Data Services]
ms.assetid: 83075cdf-f059-4646-8ba2-19be8202f130
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a411290435a10e351c05e9dd1350bde597dbe449
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289251"
---
# <a name="system-settings-master-data-services"></a>시스템 설정(Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스와 연결된 모든 웹 애플리케이션 및 웹 서비스에 대해 시스템 설정을 구성할 수 있습니다.  
  
 이러한 설정 중 대부분은 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 데이터베이스 **페이지의** 에서 구성할 수 있습니다. 다른 설정은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 시스템 설정 테이블(mdm.tblSystemSetting)에서 구성할 수 있습니다.  
  
 설정은 다음 범주별로 그룹화할 수 있습니다.  
  
-   [일반 설정](#General)  
  
-   [버전 관리 설정](#Versions)  
  
-   [준비 설정](#Staging)  
  
-   [탐색기 설정](#Explorer)  
  
-   [Excel 용 추가 기능 설정](#xls)  
  
-   [비즈니스 규칙 설정](#BusinessRules)  
  
-   [알림 설정](#Notifications)  
  
-   [보안 설정](#Security)  
  
-   [사용 되지 않음](#NotUsed)  
  
##  <a name="General"></a>일반 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
|**데이터베이스 연결 제한 시간**|**DatabaseConnectionTimeOut**|
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 연결을 완료하는 데 허용하는 시간(초)입니다. 연결이 이 시간 안에 완료되지 않으면 해당 연결이 취소되고 오류가 반환됩니다. 기본값은 **60** 초(1분)입니다.|  
|**데이터베이스 명령 제한 시간**|**DatabaseCommandTimeOut**|
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 명령을 완료하는 데 허용하는 시간(초)입니다. 명령이 이 시간 안에 완료되지 않으면 해당 명령이 취소되고 오류가 반환됩니다. 기본값은 **3600** 초 (60 분)입니다.|  
|**웹 서비스 제한 시간**|**ServerTimeOut**|ASP.NET에서 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 페이지 요청을 완료하는 데 허용하는 시간(초)입니다. 요청이 이 시간 안에 완료되지 않으면 해당 요청이 취소되고 오류가 반환됩니다. 기본값은 **120000** 초(2000분)입니다.|  
|**클라이언트 제한 시간**|**ClientTimeOut**|
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에서 아무 작업이 없는 상태가 얼마나 지속되면 홈 페이지로 돌아가는지를 지정하는 시간(초)입니다. 기본값은 **300** 초(5분)입니다.|  
|**일괄 처리당 행 수**|**RowsPerBatch**|웹 서비스를 통해 각 일괄 처리에서 검색할 레코드 수입니다. 기본값은 **50**입니다.|  
||**ApplicationName**|이벤트 로그에 표시되는 텍스트입니다. 기본값은 **MDM**입니다.|  
||**SiteTitle**|
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 브라우저의 제목 표시줄에 표시되는 텍스트입니다. 기본값은 **마스터 데이터 관리자**입니다.|  
  
##  <a name="Versions"></a>버전 관리 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
|**커밋된 버전만 복사**|**Copyonly Committedversion**|
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 사용자가 **커밋됨**상태의 모델만 복사할 수 있는지, 아니면 모든 상태의 버전을 복사할 수 있는지 결정합니다. 기본값은 **예** 또는 **1**로, 사용자가 **커밋됨** 상태의 버전만 복사할 수 있음을 나타냅니다. 사용자가 모든 버전을 복사할 수 있도록 하려면 **아니요** 또는 **2** 로 변경합니다.|  
  
 자세한 내용은 [버전&#40;Master Data Services&#41;](versions-master-data-services.md)을 참조하세요.  
  
##  <a name="Staging"></a>준비 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
|**모든 준비 트랜잭션 기록**|**StagingTransactionLogging**|SQL Server 2008 R2에만 적용됩니다. 준비 레코드가 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 로드될 때 트랜잭션을 기록할지 여부를 결정합니다. 기본값은 **해제** 또는 **2**입니다. 기록할 수 있도록 설정하려면 **설정** 또는 **1** 로 변경합니다.|  
|**준비 일괄 처리 간격**|**StagingBatchInterval**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **통합 관리** 기능 영역에서 **일괄 처리 시작** 을 선택한 후 일괄 처리가 처리될 때까지의 시간(초)입니다. 기본값은 **60** 초(1분)입니다.|  
  
 자세한 내용은 [데이터 가져오기&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)를 참조하세요.  
  
##  <a name="Explorer"></a>탐색기 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
|**기본적으로 계층의 멤버 수**|**계층 구조 Childnodelimit**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **탐색기** 기능 영역에서 **...추가...** 가 표시되기 전에 각 계층에 표시되는 최대 멤버 수입니다. 
  **...추가...** 를 클릭하여 다음 멤버 그룹을 표시할 수 있습니다. 기본값은 **50**입니다.|  
|**기본적으로 계층에 이름 표시**|**ShowNamesInHierarchy**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **탐색기** 기능 영역에서 계층을 볼 때 선택되는 기본 설정을 결정합니다.<br /><br /> 기본값은 **예** 또는 **1**로, 각 멤버의 이름 및 코드가 표시됨을 나타냅니다. 코드만 표시하려면 **아니요** 또는 **2** 로 변경합니다.|  
|**목록의 도메인 기반 특성 수**|**DBAListRowLimit**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **탐색기** 기능 영역에서 표의 도메인 기반 특성 값을 두 번 클릭할 때 목록에 표시되는 특성 수입니다. 기본값은 **50**입니다. 멤버 수가 50개보다 많으면 검색 가능한 대화 상자가 대신 표시됩니다.|  
||**GridFilterDefaultFuzzySimilarityLevel**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **탐색기** 기능 영역에서 **일치** 필터 조건을 사용할 때 사용되는 유사성 수준입니다. 기본값은 **0.3**입니다. 검색 조건과 보다 일치하는 항목을 반환하려면 **1** 에 가까운 값으로 설정합니다. 정확하게 일치하는 항목을 반환하려면 **1** 로 설정합니다.|  
  
##  <a name="xls"></a>Excel 용 추가 기능 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
|웹 사이트 홈 페이지에 Excel용 추가 기능 텍스트 표시|ShowAddInText|
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지에 사용자가 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]을 다운로드할 수 있는 링크를 표시합니다.|  
|웹 사이트 홈 페이지의 Excel용 추가 기능 설치 경로|AddInURL|
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지에 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 에 대한 링크가 표시되는 경우 해당 링크를 클릭하면 사용자가 이동하는 위치입니다.|  
  
##  <a name="BusinessRules"></a>비즈니스 규칙 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
|**새 비즈니스 규칙 증가값**|**BusinessRuleDefaultPriorityIncrement**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **시스템 관리** 기능 영역에서 각 비즈니스 규칙의 우선 순위가 증가되는 단위입니다. 기본값은 **10**입니다.|  
|**비즈니스 규칙을 적용할 멤버 수**|**BusinessRuleRealtimeMemberCount**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **탐색기** 기능 영역에서 비즈니스 규칙을 적용할 최대 멤버 수입니다. 
  [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]에서 비즈니스 규칙을 적용할 활성 워크시트에 있는 최대 멤버 수입니다. 기본값은 **10000**입니다.|  
  
 자세한 내용은 [비즈니스 규칙&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)을 참조하세요.  
  
##  <a name="Notifications"></a>알림 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
|**알림에 대 한 마스터 데이터 관리자 URL**|**MDMRootURL**|메일 알림의 링크에 사용되는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션의 URL(예: http://constoso/mds)입니다.|  
|**알림 전자 메일 간격**|**NotificationInterval**|전자 메일 알림을 보내는 빈도(초)입니다. 기본값은 **120** 초(2분)입니다.|  
|**단일 전자 메일의 알림 수**|**NotificationsPerEmail**|단일 알림 전자 메일에 나열될 유효성 검사 문제의 최대 개수입니다. 문제가 더 있더라도 전자 메일에는 포함되지 않지만 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서는 제공됩니다.|  
|**기본 전자 메일 형식**|**EmailFormat**|모든 전자 메일 알림의 형식입니다. 기본값은 **HTML** 또는 **1**입니다. 데이터베이스 설정 **2** 는 **텍스트**를 나타냅니다.<br /><br /> 참고: 개별 사용자의 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]일반 **탭에서** 전자 메일 형식 **을 변경 및 저장하여** 에서 해당 사용자에 대한 이 설정을 재정의할 수 있습니다.|  
|**전자 메일 주소에 대 한 정규식**|**EmailRegExPattern**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 사용자 **및 그룹 권한** 기능 영역에서 사용자의 **일반** 탭에 입력 한 전자 메일 주소의 유효성을 검사 하는 데 사용 되는 정규식입니다. 정규식에 대 한 자세한 내용은 MSDN library의 [정규식 언어 요소](https://go.microsoft.com/fwlink/?LinkId=164401) 를 참조 하세요.|  
|**데이터베이스 메일 계정**|**EmailProfilePrincipalAccount**|전자 메일 알림을 보낼 때 사용할 데이터베이스 메일 계정을 표시합니다. 기본 프로필은 **mds_email_user**입니다.|  
|**데이터베이스 메일 프로필**|**DatabaseMailProfile**|전자 메일 알림을 보낼 때 사용할 데이터베이스 메일 프로필입니다. 기본값은 공백입니다.|  
||**ValidationIssueHTML**|비즈니스 규칙이 유효성 검사를 통과하지 못할 경우 전자 메일 사용자에게 전달되는 HTML 형식의 텍스트입니다.|  
||**ValidationIssueText**|비즈니스 규칙이 유효성 검사를 통과하지 못할 경우 전자 메일 사용자에게 전달되는 일반 텍스트 형식의 텍스트입니다.|  
||**VersionStatusChangeText**|버전 상태가 변경될 때 전자 메일 사용자에게 전달되는 일반 텍스트 형식의 텍스트입니다. 전체 모델에 대한 **업데이트** 권한을 가진 사용자만 이 전자 메일을 받습니다.|  
||**VersionStatusChangeHTML**|버전 상태가 변경될 때 전자 메일 사용자에게 전달되는 HTML 형식의 텍스트입니다. 전체 모델에 대한 **업데이트** 권한을 가진 사용자만 이 전자 메일을 받습니다.|  
  
 자세한 내용은 [알림&#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)을 참조하세요.  
  
##  <a name="Security"></a>보안 설정  
  
|구성 관리자 설정|시스템 설정|Description|  
|-----------------------------------|--------------------|-----------------|  
||**SecurityMemberProcessInterval**|
  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **사용자 및 그룹 권한** 기능 영역에서 **계층 멤버** 탭에 설정된 해당 사용자 및 그룹 권한이 적용되는 빈도(초)입니다. 기본값은 **3600** 초 (60 분)입니다.|  
  
 자세한 내용은 [멤버 권한 즉시 적용&#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md)을 참조하세요.  
  
##  <a name="NotUsed"></a>사용 되지 않음  
 시스템 설정 테이블의 다음 설정은 사용되지 않습니다.  
  
-   **SecurityMode**  
  
-   **MDSHubName**  
  
-   **ApplicationLogging**  
  
-   **ReportServer**  
  
-   **ReportDirectory**  
  
-   **BusinessRuleEngineIterationLimit**  
  
-   **BusinessRuleExtensibility**  
  
-   **AttributeExplorerMarkAllActionMemberCount**  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 개체 보안 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/database-object-security-master-data-services.md)  
  
  
