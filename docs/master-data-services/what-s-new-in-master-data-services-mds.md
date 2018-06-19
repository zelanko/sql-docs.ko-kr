---
title: MDS(Master Data Services)의 새로운 기능 | Microsoft Docs
ms.custom: ''
ms.date: 07/08/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ad530f60-d480-4457-ba7a-93a10c8a1695
caps.latest.revision: 85
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 8f814950c08368a4045e151f4a6076f9be472e68
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328477"
---
# <a name="what39s-new-in-master-data-services-mds"></a>MDS(Master Data Services)의 새로운 기능

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[feedback-stackoverflow-msdn-connect-md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 이 항목에서는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]릴리스의 변경 내용 및 업데이트 내용을 요약합니다. 
  
 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에서 데이터를 구성하는 방법에 대한 개요는 [Master Data Services 개요](../master-data-services/master-data-services-overview-mds.md)를 참조하세요. 
  
 **Master Data Services를 설치하고, 데이터베이스 및 웹 사이트를 설정하고, 샘플 모델을 배포하려면**  [MDS(Master Data Services) 개요 ](../master-data-services/master-data-services-overview-mds.md)를 참조하세요.  
  
 **다운로드**  
  
-   [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]를 다운로드하려면  **[평가 센터](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)** 로 이동하세요.  
  
-   Azure 계정이 있으세요?  계정이 있는 경우 **[여기](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** 로 이동하여 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]이(가) 이미 설치된 가상 머신을 실행해 보세요.  
  
##  <a name="improved-performance"></a>성능 향상  
  
 성능 향상을 통해 더 큰 모델을 만들고, 데이터를 보다 효율적으로 로드하고, 전반적으로 더 나은 성능을 얻을 수 있습니다. 여기에는 데이터 로드 시간을 줄이고 추가 기능에서 더 큰 엔터티를 처리하도록 Microsoft Excel용 추가 기능의 성능이 향상된 개선 사항이 포함됩니다.  
  
 Microsoft Excel용 추가 기능에 대한 자세한 내용은 [Master Data Services Add-in for Microsoft Excel](../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)을 참조하세요.  
  
 향상된 기능은 다음과 같습니다.  
  
-   엔터티 수준에서 데이터가 압축되며 이는 기본적으로 사용하도록 설정됩니다. 데이터 압축을 사용하면 모든 엔터티 관련 테이블 및 인덱스가 SQL 행 수준 압축으로 압축됩니다. 이는 특히 마스터 데이터에 수백만 개의 행 및/또는 많은 NULL 값 열이 있는 경우 마스터 데이터를 읽거나 업데이트할 때 디스크 I/O를 크게 감소시킵니다.  
  
     SQL Server 엔진 쪽의 CPU 사용량이 약간 증가했기 때문에 서버에 바인딩된 CPU가 있는 경우 엔터티를 편집하여 데이터 압축을 해제할 수 있습니다.  
  
     자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)및 [데이터 압축](../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
-   동적 콘텐츠 압축 IIS 기능은 기본적으로 사용하도록 설정됩니다. 이로 인해 CPU 사용량이 증가하지만 xml 응답 크기가 크게 줄어들고 네트워크 I/O가 저장됩니다. 서버에 바인딩된 CPU가 있는 경우 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config 파일에 다음 설정을 추가하여 데이터 압축을 해제할 수 있습니다.  
  
    ```  
    <configuration>  
       \<system.webServer>  
          <urlCompression doStaticCompression="true" doDynamicCompression="false " />  
       \</system.webServer>  
    </configuration>  
  
    ```  
  
     자세한 내용은 [URL 압축](http://www.iis.net/configreference/system.webserver/urlcompression)을 참조하세요.  
  
-   다음 새 SQL Server 에이전트 작업은 인덱스 및 로그 유지 관리를 수행합니다.  
  
    -   MDS_MDM_Sample_Index_Maintenace  
  
    -   MDS_MDM_Sample_Log_Maintenace  
  
 기본적으로 MDS_MDM_Sample_Index_Maintenance 작업은 매주 실행됩니다. 일정을 수정할 수 있습니다. 또한 udpDefragmentation 저장 프로시저를 사용하여 언제든지 작업을 수동으로 실행할 수 있습니다. 대용량 마스터 데이터가 삽입되거나 업데이트될 때마다 또는 기존 버전에서 새 버전이 만들어진 후에 저장 프로시저를 실행하는 것이 좋습니다.  
  
 조각화가 30%를 넘는 인덱스는 온라인으로 다시 작성됩니다. 다시 작성되는 동안 같은 테이블의 CRUD 작업 성능이 저하됩니다. 성능 저하가 걱정되는 경우 업무 시간 외에 저장 프로시저를 실행하는 것이 좋습니다. 인덱스 조각화에 대한 자세한 내용은 [Reorganize and Rebuild Indexes](../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하십시오.  
  
 자세한 내용은 Master Data Services 블로그에서 [SQL Server 2016의 성능 및 배율 향상](http://go.microsoft.com/fwlink/p/?LinkId=615375)게시물을 참조하세요.  
  
##  <a name="improved-security"></a>보안 향상:  
  
 새로운 슈퍼 사용자 기능 권한은 사용자 또는 그룹에 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]이전 릴리스의 서버 관리자와 동일한 권한을 제공합니다. 슈퍼 사용자 권한은 여러 사용자 및 그룹에 할당될 수 있습니다. 이전 릴리스에서는 원래 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 를 설치한 사용자가 서버 관리자였으므로 이 권한을 다른 사용자 또는 그룹에 이전하기 어려웠습니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
 이제 사용자에게 모델 수준에서 관리자 권한이 명시적으로 할당될 수 있습니다 . 따라서 나중에 모델 하위 트리(예: 엔터티 수준)에서 사용자에게 권한이 할당된 경우 이 관리자 권한이 상실되지 않습니다.  
  
 이 릴리스의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 읽기, 만들기, 업데이트 및 삭제 권한을 도입하여 더 많은 수준의 권한을 제공합니다. 예를 들어 업데이트만 있는 사용자는 이제 데이터를 만들거나 삭제하지 않고 마스터 데이터를 업데이트할 수 있습니다. 사용자에게 만들기, 업데이트 또는 삭제 권한을 부여한 경우 해당 사용자에게는 읽기 권한이 자동으로 할당됩니다. 읽기, 만들기, 업데이트 및 삭제 권한을 결합할 수도 있습니다.  
  
 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]로 업그레이드하는 경우 다음 표와 같이 이전 권한이 새 권한으로 변환됩니다.  
  
|이전 릴리스의 권한|새 권한|  
|------------------------------------|--------------------|  
|원래 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 를 설치한 사용자가 서버 관리자 권한을 가짐|사용자가 슈퍼 사용자 기능 권한을 가짐|  
|사용자가 모델 수준에서 업데이트 권한을 가지고 모델 하위 트리에서는 권한을 가지지 않으므로 암시적으로 모델 관리자가 됨|사용자가 모델 수준에서 명시적으로 관리자 권한을 가짐|  
|사용자가 읽기 전용 권한을 가짐|사용자가 읽기 액세스 권한을 가짐|  
|사용자가 업데이트 권한을 가짐|사용자가 만들기, 업데이트, 삭제 및 읽기의 네 가지 액세스 권한을 모두 가짐|  
|사용자가 거부 권한을 가짐|사용자가 거부 권한을 가짐|  
  
 권한에 대한 자세한 내용은 [보안&#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)을 참조하세요.  
  
##  <a name="improved-transaction-log-maintenance"></a>향상된 트랜잭션 로그 유지 관리  
  
 이제 미리 결정된 간격 또는 일정에 따라 시스템 설정을 사용하여 모델 수준에서 트랜잭션 로그를 정리할 수 있습니다. 데이터 변경 및 ETL 프로세스가 많은 MDS 시스템의 경우 이러한 테이블이 기하급수적으로 증가할 수 있으므로 성능 저하 및 저장소 공간 문제가 발생할 수 있습니다.  
  
 다음과 같은 형식의 데이터를 로그에서 제거할 수 있습니다.  
  
-   지정된 일 수보다 오래된 트랜잭션 기록  
  
-   지정된 일 수보다 오래된 유효성 검사 문제 기록  
  
-   지정된 일 수 이전에 실행된 준비 일괄 처리  
  
 시스템 설정을 사용하여 모델 수준에서 트랜잭션 로그의 데이터가 제거되는 빈도를 구성할 수 있습니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md) 및 [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)를 참조하세요. 트랜잭션에 대한 자세한 내용은 [트랜잭션&#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)을 참조하세요.  
  
 SQL Server 에이전트 작업 MDS_MDM_Sample_Log_Maintenace는 트랜잭션 로그 정리를 트리거하며 매일 밤에 실행됩니다. SQL Server 에이전트를 사용하여 이 작업에 대한 일정을 수정할 수 있습니다.  
  
 또한 저장 프로시저를 호출하여 트랜잭션 로그를 정리할 수 있습니다. 자세한 내용은 [트랜잭션&#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)을 참조하세요.  
  
## <a name="improved-troubleshooting"></a>문제 해결 향상  
  
 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 디버깅을 개선하고 보다 쉽게 문제를 해결할 수 있도록 해주는 기능이 추가되었습니다. 자세한 내용은 [추적&#40;Master Data Services&#41;](../master-data-services/tracing-master-data-services.md)을 참조하세요.  
  
## <a name="improved-manageability"></a>관리 효율성 향상  
  
 관리 효율성이 향상되어 유지 관리 비용이 절감되고 ROI(투자 수익률)를 높일 수 있습니다. 이러한 향상된 기능에는 트랜잭션 로그 유지 관리 및 보안 개선뿐 아니라 다음과 같은 새로운 기능이 포함됩니다.  
  
-   50자를 초과하는 특성 이름 사용  
  
-   Name 및 Code 특성 이름 바꾸기 및 숨기기  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [모델&#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
-   [엔터티&#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [트랜잭션&#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
-   [보안&#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  

## <a name="business-rule-improvements"></a>비즈니스 규칙 개선 사항
 **비즈니스 규칙 관리(Excel용 MDS 추가 기능)**  
  
 Excel용 Master Data Services 추가 기능에서는 비즈니스 규칙 만들기 및 편집 등을 통해 비즈니스 규칙을 관리할 수 있습니다. 비즈니스 규칙은 데이터의 유효성을 검사하는 데 사용됩니다.  
 
 **비즈니스 규칙 확장**  
  
 비즈니스 규칙 조건 및 동작의 확장으로 사용자 정의 SQL 스크립트를 적용할 수 있습니다. SQL 함수를 조건으로 사용할 수 있습니다. SQL 저장 프로시저를 동작으로 사용할 수 있습니다. 자세한 내용은 [비즈니스 규칙 확장#40;Master Data Services&#41;](../master-data-services/business-rules-extension-master-data-services.md)을 참조하세요. 
 
 **비즈니스 규칙 관리 환경 다시 디자인**  
  
 환경을 개선하기 위해 MDS의 비즈니스 규칙 관리 환경이 완전히 다시 디자인되었습니다. 이 기능에 대한 자세한 내용은 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)을 참조하세요.  
  
 **Excel용 MDS 추가 기능에서 제거된 비즈니스 규칙 관리 기능**  
  
 환경을 다시 디자인했기 때문에 Excel용 MDS 추가 기능에서 비즈니스 규칙 관리 기능이 제거되었습니다.    

 **새로운 비즈니스 규칙 조건**  
  
 전체 조건 집합을 제공하기 위해 7개의 새로운 비즈니스 규칙 조건이 추가되었습니다. 자세한 내용은 [비즈니스 규칙 조건&#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)을 참조하세요.  

## <a name="derived-hierarchy-improvements"></a>파생 계층 개선 사항

 **파생 계층의 다 대 다 관계**  
  
 이제 다 대 다 관계를 표시하는 파생 계층을 만들 수 있습니다. 두 엔터티 간의 매핑을 제공하는 세 번째 엔터티를 사용하여 두 엔터티 간의 다 대 다 관계를 모델링할 수 있습니다. 매핑 엔터티는 다른 엔터티를 참조하는 둘 이상의 도메인 기반 특성이 있는 엔터티입니다.  
  
 예를 들어 엔터티 M에는 A를 참조하는 도메인 기반 특성과 B를 참조하는 도메인 기반 특성이 있습니다. 매핑 엔터티를 사용하여 A와 B 간의 계층 구조를 만들 수 있습니다.  
  
 자세한 내용은 [파생 계층에서 다 대 다 관계 표시&#40;Master Data Services&#41;](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md)를 참조하세요.  
 
 **파생 계층에서 다 대 다 관계 편집**  
  
 매핑 엔터티 멤버를 수정하여 다 대 다 관계를 편집할 수 있습니다. 자세한 내용은 [파생 계층에서 다 대 다 관계 표시&#40;Master Data Services&#41;](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md)를 참조하세요.  
 
 **파생 계층 관리 환경 개선**  
  
 MDS의 파생 계층 관리 환경이 개선되었습니다. 이 기능에 대한 자세한 내용은 [파생 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)를 참조하세요.  
  
 환경을 다시 디자인했기 때문에 Excel용 MDS 추가 기능에서 비즈니스 규칙 관리 기능이 제거되었습니다.  
 
## <a name="attribute-improvements"></a>특성 개선 사항   
    
 **사용자 지정 인덱스**  
  
 엔터티에서 하나의 속성(단일 인덱스) 또는 속성 목록(복합 인덱스)에 대한 비클러스터형 인덱스를 만들어 쿼리 성능을 개선할 수 있습니다. 자세한 내용은 [사용자 지정 인덱스&#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)를 참조하세요.  
 
  **특성 필터**  
  
 리프 멤버에 대한 도메인 기반 특성의 경우 필터 부모 특성을 사용하여 도메인 기반 특성에 허용되는 값을 제한할 수 있습니다. 자세한 내용은 [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)를 참조하세요.  
 
## <a name="entity-and-member-improvements"></a>엔터티 및 멤버 개선 사항 
  
 **엔터티 동기화 관계**  
  
 엔터티 동기화 관계를 만들어 서로 다른 모델 간의 엔터티 데이터를 공유할 수 있습니다. 자세한 내용은 [엔터티 동기화 관계&#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md)를 참조하세요.  
  
 **일시 삭제된 멤버 삭제**  
  
 이제 모델 버전에서 일시 삭제된 모든 멤버를 제거(영구적으로 삭제)할 수 있습니다. 멤버 삭제는 멤버를 비활성화하거나 일시적으로 삭제할 뿐입니다. 자세한 내용은 [버전 멤버 삭제&#40;Master Data Services&#41;](../master-data-services/purge-version-members-master-data-services.md)를 참조하세요.  
 
## <a name="improvements-for-managing-changes"></a>변경 내용 관리 개선 사항 
  
 **멤버 수정 기록**  
  
 멤버가 변경된 경우 멤버 수정 기록이 작성됩니다. 수정 기록을 롤백할 뿐만 아니라 수정 내용을 보고 주석을 추가할 수 있습니다. **Log Retention Days** 속성을 사용하여 기록 데이터를 보존할 기간을 지정할 수 있습니다. 자세한 내용은 [멤버 수정 기록&#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)을 참조하세요.  
  
 **병합 충돌**  
  
 다른 사용자가 변경한 데이터를 게시하려고 하면 충돌 오류로 인해 게시에 실패합니다. 이 오류를 해결하려면 병합 충돌을 수행하고 변경 내용을 다시 게시합니다. 자세한 내용은 [병합 충돌(Master Data Services)](../master-data-services/merge-conflicts-master-data-services.md) 및 [병합 충돌(Excel용 MDS 추가 기능)](../master-data-services/microsoft-excel-add-in/merge-conflicts-mds-add-in-for-excel.md)을 참조하세요.  
  
 **변경 집합**  
  
 변경 집합을 사용하여 보류 중인 변경 내용을 엔터티를 저장하고 보류 중인 변경 내용을 확인 및 수정할 수 있습니다. 엔터티에 변경 내용에 대한 승인이 필요한 경우 보류 중인 변경 내용을 변경 집합에 저장하고 관리자의 승인을 위해 제출해야 합니다. 자세한 내용은 [변경 집합&#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md)을 참조하세요.  
  
 **변경 집합 전자 메일 및 관리**  
  
 이 릴리스에서는 이제 모델 및 버전별로 모든 변경 내용을 보고 관리할 수 있습니다. 또한 승인이 필요한 엔터티에 대해 변경 집합 상태가 변경될 때마다 전자 메일 알림이 제공됩니다. 자세한 내용은 [변경 집합 관리&#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md) 및 [알림&#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)을 참조하세요.  
  
 **수정 기록 보기 및 관리**  
  
 엔터티 및 멤버별로 수정 기록을 보고 관리할 수 있습니다. 업데이트 권한이 있는 경우 멤버를 이전 버전으로 롤백할 수 있습니다. 자세한 내용은 [멤버 수정 기록&#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)을 참조하세요.  
 
## <a name="tool-and-sample-improvements"></a>도구 및 샘플 개선 사항 
  
 **Excel용 MDS 추가 기능에서 쿼리 파일 저장 또는 열기**  
  
 엔터티 탐색기 페이지에서 **Excel** 을 클릭하여 바로 가기 쿼리 파일을 저장할 수 있습니다. 또는 Excel용 MDS 추가 기능에서 컴퓨터에 저장된 쿼리 파일을 열 수 있습니다. QueryOpener 응용 프로그램을 사용하여 저장된 파일을 열 수 있습니다. 자세한 내용은 [바로 가기 쿼리 파일&#40;Excel용 MDS 추가 기능&#41;](../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)을 참조하세요.  
  
 쿼리 파일에는 탐색기 페이지의 필터 및 계층 정보가 포함됩니다.  
   
 **샘플 모델 배포 패키지 업데이트**  
  
 샘플 패키지가 새로운 시나리오를 지원하도록 업데이트되었습니다. 자세한 내용은 [SQL Server 예제: 모델 배포 패키지(MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 버전에서 지원하는 Master Data Services 및 Data Quality Services 기능](../master-data-services/master-data-services-and-data-quality-services-features-support.md)  
 [사용되지 않는 Master Data Services 기능](../master-data-services/deprecated-master-data-services-features.md)   
 [지원되지 않는 MDS(Master Data Services) 기능](../master-data-services/discontinued-master-data-services-features.md)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

