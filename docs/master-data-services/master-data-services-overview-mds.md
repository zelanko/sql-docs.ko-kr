---
title: "MDS(Master Data Services) 개요 | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- what is master data
helpviewer_keywords:
- Master Data Services, overview
- Master Data Services
ms.assetid: 8a4c28b1-6061-4850-80b6-132438b8c156
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Active
ms.openlocfilehash: a60fddbc00fa808590a06bc3263dfe6bc966f18b
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
# <a name="master-data-services-overview-mds"></a>MDS(Master Data Services) 개요
  이 항목에서는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]의 주요 데이터 구성 및 관리 기능을 설명합니다. 
  
 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 사용하면 조직 데이터의 마스터 집합을 관리할 수 있습니다. 데이터를 모델로 구성하고, 데이터를 업데이트하는 규칙을 만들고, 데이터를 누가 업데이트하는지 제어할 수 있습니다. Excel을 사용하면 조직의 다른 사람들과 마스터 데이터 집합을 공유할 수 있습니다. 
  
 >  [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 아키텍처에 대한 설명은 simple-talk.com의 [Master Data Services -- The Basics](https://www.simple-talk.com/sql/database-delivery/master-data-services-basics) (Master Data Services -- 기본 사항) 문서를 참조하세요. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 새로운 기능에 대한 자세한 내용은 [MDS&#40;Master Data Services&#41;의 새로운 기능](../master-data-services/what-s-new-in-master-data-services-mds.md)을 참조하세요.  
   **[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치하고, 데이터베이스 및 웹 사이트를 설정하고, 샘플 모델을 배포하는 방법에 대한 자세한 내용은** [Master Data Services 설치 및 구성](../master-data-services/master-data-services-installation-and-configuration.md)을 참조하세요.  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델은 마스터 데이터의 구조에서 가장 높은 수준의 컨테이너입니다. 온라인 제품 데이터를 관리하는 등의 목적으로 유사한 데이터의 그룹을 관리하기 위해 모델을 만듭니다. 모델에는 하나 이상의 엔터티가 포함되며 엔터티에는 데이터 레코드인 멤버가 포함됩니다. 엔터티는 테이블과 비슷합니다.  
  
 예를 들어 온라인 제품 모델에는 제품, 색상, 스타일 등의 엔터티가 포함될 수 있습니다. 색상 엔터티에는 빨간색, 은색 및 검은색에 대한 멤버가 포함될 수 있습니다.  
  
 ![색상 엔터티](../master-data-services/media/mds-productmodel-colorentity-composite.png "색상 엔터티")  
  
 모델에는 엔터티 내에서 정의된 특성도 포함됩니다. 특성에는 엔터티 멤버를 설명하는 데 도움이 되는 값이 포함됩니다. 자유 형식 특성과 도메인 기반 특성이 있습니다.  도메인 기반 특성에는 엔터티의 멤버로 채워지고 다른 엔터티의 특성 값으로 사용될 수 있는 값이 포함됩니다.  
  
 예를 들어 제품 엔터티에는 비용 및 무게에 대한 자유 형식 특성이 있을 수 있습니다. 또한 색상 엔터티 멤버로 채워지는 값이 포함된 색상 ![번호 1](../master-data-services/media/mds-number1.png "번호 1")에 대한 도메인 기반 특성이 있습니다. 이러한 색상의 마스터 목록은 제품 엔터티 ![번호 2](../master-data-services/media/mds-number2.png "번호 2")의 특성 값으로 사용됩니다.  
  
 ![색에 대한 도메인 기반 특성](../master-data-services/media/mds-productentity-color-domainattribute.png "색에 대한 도메인 기반 특성")  
  
 파생 계층은 모델의 엔터티 간 관계에서 제공됩니다. 이러한 관계는 도메인 기반 특성 관계입니다. 예를 들어 제품 모델에서는 색상 ![번호 2](../master-data-services/media/mds-number2.png "번호 2") 및 제품 ![번호 3](../master-data-services/media/mds-number3.png "번호 3") 엔터티 간의 관계에서 제공되는 색상 파생 계층 ![번호 1](../master-data-services/media/mds-number1.png "번호 1")이 있을 수 있습니다.  
  
 ![색상 파생 계층](../master-data-services/media/mds-derivedhierarchy.png "색상 파생 계층")  
  
 데이터에 대한 기본 구조를 정의한 후 가져오기 기능을 사용하여 데이터 레코드(멤버)의 추가를 시작할 수 있습니다. 준비 표에 데이터를 로드하고, 비즈니스 규칙을 사용하여 데이터의 유효성을 검사하고, MDS 표에 데이터를 로드합니다.  비즈니스 규칙을 사용하여 특성 값을 설정할 수도 있습니다.  
  
 다음 표에 주요 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 작업이 정리되어 있습니다. 다른 언급이 없는 경우 아래의 모든 절차를 수행하려면 사용자가 모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
> [!NOTE]  
>  테스트 환경에서 다음 태스크를 완료하고 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치할 때 제공된 샘플 데이터를 사용할 수 있습니다. 자세한 내용은 [모델 배포&#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)를 참조하세요.  
  
|작업|세부 정보|관련 항목|  
|------------|-------------|--------------------|  
|모델 만들기|모델을 만들면 VERSION_1로 간주됩니다.|[모델&#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)<br /><br /> [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)|  
|엔터티 만들기|멤버를 포함하는 데 필요한 만큼 엔터티를 만듭니다.|[엔터티&#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)<br /><br /> [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)|  
|도메인 기반 특성으로 사용할 엔터티 만들기|도메인 기반 특성을 만들려면 먼저 엔터티를 만들어 특성 값 목록을 채웁니다.|[도메인 기반 특성&#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)<br /><br /> [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|엔터티에 대한 특성 만들기|멤버를 설명하기 위해 특성을 만듭니다. 이름 및 코드 특성은 각 엔터티에 자동으로 포함되며 제거할 수 없습니다. 다른 자유 형식 특성을 만들어 텍스트, 날짜, 숫자 또는 파일을 포함할 수 있습니다.|[특성&#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)<br /><br /> [텍스트 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)<br /><br /> [숫자 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md)<br /><br /> [날짜 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-date-attribute-master-data-services.md)<br /><br /> [링크 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-link-attribute-master-data-services.md)<br /><br /> [파일 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|특성 그룹 만들기|엔터티에 대한 4개 또는 5개 이상의 특성이 있는 경우 특성 그룹을 만들 수 있습니다. 이러한 그룹은 **탐색기** 에서 표 위에 탭으로 표시되며, 여러 특성을 손쉽게 탐색할 수 있도록 각 탭으로 그룹화합니다.|[특성 그룹&#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)<br /><br /> [특성 그룹 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|지원 엔터티를 위한 멤버 가져오기|준비 프로세스를 사용하여 지원 엔터티에 대한 데이터를 가져옵니다. 제품 모델의 경우 색이나 크기를 가져올 수 있습니다. 멤버를 직접 만들 수도 있습니다.<br /><br /> <br /><br /> 참고: 사용자는 엔터티의 리프 모델 개체에 대한 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 업데이트 **이상의 사용 권한과** 탐색기 **기능 영역에 대한 액세스 권한이 있는 경우** 에서 멤버를 만들 수 있습니다.|[개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)<br /><br /> [리프 멤버 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|데이터 품질을 보장하기 위한 비즈니스 규칙 만들기 및 적용|데이터의 정확성을 보장하는 비즈니스 규칙을 만들고 게시합니다. 다음과 같은 작업을 위해 비즈니스 규칙을 사용할 수 있습니다.<br /><br /> 기본 특성 값을 설정합니다.<br /><br /> 특성 값을 변경합니다.<br /><br /> 데이터가 비즈니스 규칙 유효성 검사에 실패한 경우 전자 메일 알림을 보냅니다.|[비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)<br /><br /> [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)<br /><br /> [비즈니스 규칙에 대해 특정 멤버 유효성 검사(Master Data Services)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)<br /><br /> [메일 알림 구성&#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)<br /><br /> [알림을 보내도록 비즈니스 규칙 구성&#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|기본 엔터티에 대한 멤버 가져오기 및 비즈니스 규칙 적용|준비 프로세스를 사용하여 기본 엔터티에 대한 멤버를 가져옵니다. 작업이 끝나면 버전의 유효성을 검사하여 비즈니스 규칙을 모델 버전의 모든 멤버에 적용합니다.<br /><br /> 그런 다음 모든 비즈니스 규칙 유효성 검사 문제를 해결할 수 있습니다.|[유효성 검사&#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)<br /><br /> [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)<br /><br /> [유효성 검사 저장 프로시저&#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)|  
|파생 계층 만들기|비즈니스 요구 사항이 변화함에 따라 파생 계층을 업데이트하여 모든 멤버를 적절한 수준으로 처리할 수 있습니다.|[파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)<br /><br /> [파생 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|필요한 경우 명시적 계층을 만듭니다.|수준 기반이 아니고 단일 엔터티의 멤버를 포함하는 계층을 만들려면 명시적 계층을 만들 수 있습니다.|[명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)<br /><br /> [명시적 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|필요한 경우 컬렉션을 만듭니다.|전체 계층이 필요 없고 보고나 분석을 위해 멤버의 다른 그룹을 보려는 경우에 컬렉션을 만듭니다.<br /><br /> <br /><br /> 참고: 사용자는 컬렉션 모델 개체에 대한 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 업데이트 **이상의 사용 권한과** 탐색기 **기능 영역에 대한 액세스 권한이 있는 경우** 에서 컬렉션을 만들 수 있습니다.|[컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)<br /><br /> [컬렉션 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|사용자 정의 메타데이터 만들기|모델 개체를 설명하기 위해 사용자 정의 메타데이터를 모델에 추가합니다. 메타데이터는 개체 소유자나 데이터가 제공된 원본을 포함할 수 있습니다.||  
|모델 버전 잠금 및 버전 플래그 할당|관리자를 제외하고 멤버를 변경할 수 없도록 모델 버전을 잠급니다. 비즈니스 규칙과 비교하여 버전 데이터에 대한 유효성 검사에 성공한 경우 버전을 커밋할 수 있으며 이렇게 하면 모든 사용자가 멤버를 변경할 수 없게 됩니다.<br /><br /> 버전 플래그를 만들어 모델에 할당합니다. 플래그는 사용자 및 구독 시스템이 사용할 모델 버전을 식별하는 데 유용합니다.|[버전&#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)<br /><br /> [버전 잠금&#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)<br /><br /> [버전 플래그 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)|  
|구독 뷰 만들기|구독 시스템에서 마스터 데이터를 사용하도록 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 표준 뷰를 만드는 구독 뷰를 만듭니다.|[개요: 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)<br /><br /> [구독 뷰를 만들어 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|사용자 및 그룹 권한 구성|테스트 환경에서 프로덕션 환경으로 사용자 및 그룹 권한을 복사할 수 없습니다. 그러나 테스트 환경을 사용하여 프로덕션에서 최종적으로 사용할 보안을 결정할 수 있습니다.|[보안&#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)<br /><br /> [그룹 추가&#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)<br /><br /> [사용자 추가&#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)|  
  
 준비가 끝나면 데이터를 포함하거나 포함하지 않는 모델을 프로덕션 환경에 배포할 수 있습니다. 자세한 내용은 [모델 배포&#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)를 참조하세요.  
  
  

